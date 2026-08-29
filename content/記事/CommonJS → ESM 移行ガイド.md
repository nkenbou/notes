---
title: "CommonJS → ESM 移行ガイド"
permalink: 7913d630a3e4
created: 2026-02-28
modified: 2026-03-01
tags:
  - NextJS
  - CommonJS
  - ESM
  - Jest
  - Prisma
  - TypeScript
  - jest-prisma
---
## 1. 概要・背景

### 移行の動機

Node.js エコシステム全体が ESM (ECMAScript Modules) へ移行している。本プロジェクトで移行を実施した主な理由は以下の通り。

- **Prisma v6+** が ESM ネイティブに対応し、`moduleFormat = "esm"` 設定が利用可能になった
- **Jest v30** で ESM サポートが改善され、`jest.unstable_mockModule` が安定化した
- `"type": "module"` を設定することでパッケージの意図が明確になり、CJS/ESM の混在による予期しない挙動を排除できる
- `moduleResolution: "bundler"` により、相対インポートで拡張子を書かなくてよくなり、TypeScript の記述がシンプルになる

### 対象アーキテクチャ

- **モノレポ管理**: Turborepo + pnpm workspaces
- **フロントエンド**: Next.js 15 (`apps/myapp`)
- **バックエンド/共通**: 複数の TypeScript パッケージ (`packages/auth`, `packages/myapp-query`, `packages/another-query`, etc.)
- **ORM**: Prisma (`packages/myapp-prisma`, `packages/another-prisma`)
- **テスト**: Jest + ts-jest + `@quramy/jest-prisma-node`

---

## 2. 変更ファイル一覧（チェックリスト形式）

### TypeScript 設定 (`packages/typescript-config/`)

- [ ] **`base.json`**

  - `"module": "nodenext"` → `"esnext"`
  - `"moduleResolution": "nodenext"` → `"bundler"`

- [ ] **`nextjs.json`**
  - `module` / `moduleResolution` の重複記述を削除（`base.json` から継承されるため不要）

### 各パッケージ `package.json`

- [ ] `"type": "module"` を追加（全パッケージ・全アプリ）
- [ ] `unit` スクリプトを以下に変更:
  ```json
  "unit": "NODE_OPTIONS='--experimental-vm-modules' jest"
  ```
- [ ] Jest 関連パッケージのバージョンアップ:
  - `jest`: `^29` → `^30`
  - `@types/jest`: `^29` → `^30`
  - `@jest/globals`: 新規追加 `^30`
  - `ts-jest`: 最新版に更新
- [ ] `@quramy/jest-prisma` / `@quramy/jest-prisma-node`: `^1.7` → `^1.8.2`
- [ ] `@quramy/prisma-fabbrica`: `^2.0` → `^2.3`
- [ ] `@prisma/client` / `prisma`: `^6.3` → `^6.16`
- [ ] **Prisma パッケージのみ**: `ts-node` 依存を削除、seed スクリプトを `tsx` に変更:
  ```json
  "seed": "tsx prisma/seed.ts"
  ```
- [ ] **Next.js アプリのみ**: `@prisma/nextjs-monorepo-workaround-plugin` を削除

### `tsconfig.json` / `tsconfig.build.json` (各パッケージ)

- [ ] **`tsconfig.json`**: `"types": ["@types/jest"]` を削除（理由はセクション 4「`@types/jest` と `@jest/globals` の型競合」を参照）
- [ ] **`tsconfig.build.json`**:
  - `"types": ["node"]` を追加
    > `tsconfig.json` では `types` を指定しないことで全 `@types/*` を自動読み込みしている（`@types/jest` を含む）。ビルド成果物に jest の型が混入しないよう、`tsconfig.build.json` では `@types/node` のみに制限する。
  - `"exclude": ["src/**/*.test.ts"]` を追加
    > `"types": ["node"]` でビルド時に `@types/jest` を除外すると、テストファイル内で使われる `describe` / `jest` 等の型が解決できずエラーになる。テストファイル自体をビルド対象から外すことで回避する。

### Jest 設定 (`jest.config.ts`)

- [ ] `extensionsToTreatAsEsm: [".ts"]` を追加
  > Jest のモジュールローダーは `.js` ファイルのみ `package.json` の `"type": "module"` を参照して ESM/CJS を判定する。`.ts` のような非 `.js` 拡張子はこの判定対象外で、`extensionsToTreatAsEsm` に含まれていなければ CJS として扱われる。ts-jest の `useESM: true` は ESM 構文を出力するため、Jest 側でも `.ts` を ESM として実行するよう明示が必要になる。
- [ ] transform 設定を `useESM: true` に変更:
  ```typescript
  transform: {
    "^.+\\.ts$": ["ts-jest", { useESM: true }],
  }
  ```
- [ ] `moduleNameMapper` でサブパスインポートをマッピング:
  ```typescript
  moduleNameMapper: {
    "^#domain/(.*)$": "<rootDir>/src/domain/$1",
    "^#processor/(.*)$": "<rootDir>/src/processor/$1",
    "^#interface-adapter/(.*)$": "<rootDir>/src/interface-adapter/$1",
  }
  ```
  > **なぜ必要か**: CJS モードでは `require("#domain")` の解決を Node.js が担い、`package.json` の `"imports"` フィールドをネイティブサポートしているため設定不要だった。ESM モード（`--experimental-vm-modules`）では Jest 独自の `jest-resolve` がモジュール解決を担うが、`jest-resolve` は `"imports"` フィールドを実装していない。そのため `import "#domain"` が解決できずエラーになる。`moduleNameMapper` は `jest-resolve` による探索より前に評価されるため、`"imports"` フィールドを使わずに直接マッピングして回避する。

### `.jest/setupAfterEnv.ts`

- [ ] インポート元を変更:

  ```typescript
  // Before
  import { PrismaClient } from "@myapp/myapp-prisma/client";
  import { initialize } from "@quramy/jest-prisma-node";

  // After
  import { initialize } from "@quramy/jest-prisma-node";
  import { PrismaClient } from "@myapp/myapp-prisma/prisma-client";
  ```

  > `initialize` を `PrismaClient` より**前**にインポートする順序が重要

### Prisma スキーマ (`prisma/schema.prisma`)

- [ ] generator の `provider` を変更:

  ```prisma
  // Before
  provider = "prisma-client-js"

  // After
  provider = "prisma-client"
  ```

- [ ] `prisma-client` ジェネレーターに `moduleFormat = "esm"` を追加:
  ```prisma
  generator client {
    provider     = "prisma-client"
    output       = "../.prisma"
    moduleFormat = "esm"
  }
  ```
- [ ] `prisma-fabbrica` ジェネレーターにも `moduleFormat = "esm"` を追加:
  ```prisma
  generator fabbrica {
    provider     = "prisma-fabbrica"
    output       = "../src/__generated__/fabbrica"
    moduleFormat = "esm"
  }
  ```

### Prisma パッケージの `package.json` exports 設定

- [ ] `"./prisma-client"` エクスポートを追加:

  ```json
  "exports": {
    "./client": "./src/client.ts",
    "./prisma-client": "./.prisma/client.ts",
    "./factories": "./src/factories.ts"
  }
  ```

  各エントリの責務は明確に分離されている:

  - **`./client`** → `prisma` シングルトンのみを export (`src/client.ts`)
  - **`./prisma-client`** → `PrismaClient` クラス・`Prisma` 名前空間のみを export (`.prisma/client.ts` を直接マップ)

  > **なぜ分割するか**:
  > `jest.unstable_mockModule` はモジュール全体を置き換えるため、`client` モジュールに `PrismaClient` も含めていると、モック後に `PrismaClient` が消えてしまう（詳細は [セクション 4「`jest.unstable_mockModule` はモジュール全体を置き換える」](#jest-unstable_mockmodule-はモジュール全体を置き換える) を参照）。
  > `prisma-client` を別エントリとして独立させることで、`client` をモックしても `PrismaClient` は影響を受けない。

### インポートパスの変更（Prisma パッケージ内）

- [ ] `src/client.ts`:

  ```typescript
  // Before
  export { PrismaClient, Prisma } from "../.prisma";

  // After
  export { PrismaClient, Prisma } from "../.prisma/client";
  ```

### Next.js 設定 (`next.config.mjs`)

- [ ] `PrismaPlugin` のインポートと使用を削除

---

## 3. テストコードの変更パターン

### `jest.mock` → `jest.unstable_mockModule`

ESM ではモジュールが静的に評価されるため、CJS の `jest.mock` は使えない。

```typescript
// Before (CJS)
jest.mock("@myapp/myapp-prisma/client", () => ({ prisma: jestPrisma.client }));

// After (ESM)
jest.unstable_mockModule("@myapp/myapp-prisma/client", () => {
  return { prisma: jestPrisma.client };
});
```

### 動的インポート (`await import()`)

`jest.unstable_mockModule` を呼んだ後、テスト対象モジュールを `await import()` で読み込む。
**`jest.unstable_mockModule` は `await import()` の前に呼ぶこと。**

```typescript
// jest.unstable_mockModule を呼んだ後
const { prisma } = await import("@myapp/myapp-prisma/client");
const { SomeClass } = await import("./some-module");
```

> モックしたモジュールを推移的に import しているクラス（SUT）も `await import()` で読み込む必要がある。

### Jest グローバルの明示的インポート

ESM では `jest.unstable_mockModule` などの ESM 専用 API を使うために、`jest` オブジェクトを `@jest/globals` から明示的にインポートする必要がある。

```typescript
import { jest } from "@jest/globals";
```

> この import を追加すると `@types/jest` が提供するグローバルの `jest` 型と競合するため、`tsconfig.json` の `types` から `"@types/jest"` を削除する（詳細はセクション 4「`@types/jest` と `@jest/globals` の型競合」を参照）。

### `jest.fn()` の型注釈

```typescript
// Before
const mockFn = jest.fn();

// After（型を明示して型安全にする）
const mockFn = jest.fn<SomeInterface["methodName"]>();
```

---

## 4. 落とし穴と注意点

### `jest.unstable_mockModule` の呼び出し順序

`jest.unstable_mockModule` は必ず `await import()` の**前**に呼ばなければならない。
CJS の `jest.mock` はファイル先頭に自動的にホイスティングされるが、`jest.unstable_mockModule` はホイスティングされない。

```typescript
// NG: import の後でモックを設定しても効かない
const { SomeClass } = await import("./some-module");
jest.unstable_mockModule("./dependency", () => ({ ... })); // 遅すぎる

// OK: モックを先に設定してから import する
jest.unstable_mockModule("./dependency", () => ({ ... }));
const { SomeClass } = await import("./some-module");
```

### `jest.unstable_mockModule` はモジュール全体を置き換える

`jest.unstable_mockModule` ではファクトリが返すオブジェクトが**そのモジュールの全エクスポート**になる。部分モックはできない:

```typescript
jest.unstable_mockModule("@myapp/myapp-prisma/client", () => {
  // { prisma: ... } だけ返すと、このモジュールから PrismaClient は消える
  return { prisma: jestPrisma.client };
});
```

CJS の `jest.mock` でも同様に全体置き換えだが、次の理由で問題が顕在化しなかった:

1. **実行順序**: `setupFilesAfterEnv`（`setupAfterEnv.ts`）はテストファイルより先に実行される。`jest.mock` はテストファイル内でホイスティングされるが、それはあくまで「テストファイル内の import より前」であり、`setupAfterEnv.ts` の実行より前にはならない。そのため `setupAfterEnv.ts` は実際のモックが登録される前に `PrismaClient` の実体を取得できていた。
2. **CJS の値スナップショット**: CJS の `require` は値をその場でバインドする。`setupAfterEnv.ts` が `PrismaClient` を取得した後でモジュールが置き換えられても、すでにバインドされた変数には影響しない。
3. **型のみの使用**: `PrismaClientManager` は `PrismaClient` / `Prisma` を TypeScript の型注釈としてのみ使用しており、ランタイム値としては使用していなかった。そのためモックで `undefined` になっても実行時エラーが発生しなかった。

ESM では上記の保護がすべて失われる:

- `jest.unstable_mockModule` は `await import()` と組み合わせて使うため、`setupAfterEnv.ts` の静的 import より後にモックが効く保証がない
- `PrismaClient` を `./client` エントリに残したままだと、ESM の動作によっては `setupAfterEnv.ts` でも `undefined` になりうる

**解決策**: エクスポートエントリポイントを責務で分離する（[セクション 2「Prisma パッケージの exports 設定」](#prisma-パッケージの-packagejson-exports-設定) を参照）:

- テストでモックするエントリ (`./client`) にはモック対象の export のみ入れる
- `PrismaClient` など型・クラスは独立したエントリ (`./prisma-client`) から提供する
- `setupAfterEnv.ts` は `./prisma-client` から import するため、`./client` のモックに影響されない

### `@prisma/nextjs-monorepo-workaround-plugin` は不要に

ESM 移行後、`@prisma/nextjs-monorepo-workaround-plugin` は不要になる。`next.config.mjs` から削除し、依存関係からも削除する。

### `@types/jest` と `@jest/globals` の型競合

ESM 専用 API（`jest.unstable_mockModule` 等）を使うために `@jest/globals` から `jest` を import すると、`@types/jest` がグローバルスコープに注入している `jest` 型と二重定義になり TypeScript エラーが発生する。

```
Duplicate identifier 'jest'. ts(2300)
```

**解決策**: `tsconfig.json` の `types` から `"@types/jest"` を削除する。

```jsonc
// Before
{ "compilerOptions": { "types": ["@types/jest"] } }

// After（types フィールド自体を削除）
{ "compilerOptions": {} }
```

これにより `@types/jest` によるグローバル ambient 宣言が抑制され、`@jest/globals` からの import が唯一の型ソースになる。

> `describe` / `it` / `expect` / `beforeEach` などのテストグローバルは `@types/jest` がアンビエント宣言している。`types` を削除しても `@types/jest` パッケージが `node_modules` に存在する限り TypeScript は自動的に読み込むため（`types` 未指定時は全 `@types/*` が対象）、これらのグローバル型は引き続き使用できる。

### `initialize` のインポート順序 (jest-prisma)

`.jest/setupAfterEnv.ts` で `@quramy/jest-prisma-node` の `initialize` を `PrismaClient` より**前**にインポートする必要がある。ESM では import の副作用の実行順序が import 文の記述順に依存するため、この順序が重要になる。

```typescript
// OK: initialize が先
import { initialize } from "@quramy/jest-prisma-node";
import { PrismaClient } from "@myapp/myapp-prisma/prisma-client";

// NG: PrismaClient が先だと jest-prisma の初期化が間に合わない
import { PrismaClient } from "@myapp/myapp-prisma/prisma-client";
import { initialize } from "@quramy/jest-prisma-node";
```

---

## 5. 移行手順（ステップバイステップ）

1. **依存パッケージのアップデート**

   - 全パッケージの `package.json` で Jest 関連・Prisma 関連のバージョンを更新する
   - `pnpm install` を実行してロックファイルを更新する

2. **TypeScript 設定の変更**

   - `packages/typescript-config/base.json` の `module` / `moduleResolution` を変更する
   - `packages/typescript-config/nextjs.json` から重複項目を削除する

3. **全パッケージに `"type": "module"` を追加**

   - 各 `package.json` に `"type": "module"` を追加する

4. **各パッケージの `tsconfig.json` / `tsconfig.build.json` を更新**

   - `tsconfig.json` から `"types": ["@types/jest"]` を削除する
   - `tsconfig.build.json` に `"types": ["node"]` と `"exclude"` を追加する

5. **Prisma スキーマを更新してクライアントを再生成**

   - `prisma/schema.prisma` の `provider` と `moduleFormat` を更新する
   - `prisma generate` を実行して ESM 形式のクライアントを生成する

6. **Prisma パッケージの `exports` とインポートパスを更新**

   - `package.json` に `"./prisma-client"` エクスポートを追加する
   - `src/client.ts` のインポートパスを `"../.prisma/client"` に変更する

7. **Jest 設定を更新**

   - 各パッケージの `jest.config.ts` を ESM 対応に更新する（`extensionsToTreatAsEsm`, `useESM: true`, `moduleNameMapper`）
   - `unit` スクリプトを `--experimental-vm-modules` 付きに変更する

8. **テストコードを ESM スタイルに書き換え**

   - `jest.mock` → `jest.unstable_mockModule` に変更する
   - モジュール読み込みを `await import()` に変更する
   - `import { jest } from "@jest/globals"` を追加する

9. **`.jest/setupAfterEnv.ts` を更新**

   - インポート元とインポート順序を修正する

10. **Next.js 設定を更新**

    - `next.config.mjs` から `PrismaPlugin` を削除する

11. **動作確認**
    - `pnpm -r test` でテストが全パス することを確認する
    - `pnpm build`（Next.js）が成功することを確認する
    - VRT スナップショットを更新する（`pnpm test:vrt` など）
