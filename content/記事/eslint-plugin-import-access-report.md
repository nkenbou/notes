---
permalink: 665da73517c2
tags:
  - eslint-plugin-import-access
  - Turborepo
---
# eslint-plugin-import-access で外部パッケージからの import を制御できるか調査

## 1. 調査目的

pnpm workspace monorepo において、**別パッケージ（外部パッケージ）からの import を `eslint-plugin-import-access` で制御できるか**を検証する。

具体的には、あるアプリパッケージからライブラリパッケージの内部モジュールを import した場合に、ESLint 警告を出せるかを確かめる。

## 2. 環境

- pnpm workspace monorepo（Turborepo）
- `eslint-plugin-import-access` v2.2.2
- `typescript-eslint` v8.x（type-aware linting 有効）
- `moduleResolution: "bundler"`、`"type": "module"`（ESM）

## 3. 設定

- `packages/typescript-config/base.json`: TypeScript Language Service Plugin として `eslint-plugin-import-access` を設定
- `packages/typescript-config/nextjs.json`: `defaultImportability: "package"` を追加
- `packages/eslint-config/next.js`: ESLint ルール `import-access/jsdoc` + `defaultImportability: "package"` を設定
- ライブラリパッケージの `package.json` exports: `"./*": "./dist/*.js"` でワイルドカード公開

## 4. 検証内容

アプリパッケージからライブラリパッケージの内部モジュール（例: `@example/lib/domain/domain-error`）の `DomainError` を import した。この import に対して `import-access/jsdoc` 警告が出るかを確認した。

## 5. 調査結果

### TypeScript Language Service Plugin は機能している

ライブラリパッケージをビルドすると、アノテーションのない export に `/** @private */` が付加された `.d.ts` が生成される。

```ts
// dist/domain/domain-error.d.ts
/**
 * @private
 */
export declare class DomainError extends Error { ... }
```

### ESLint プラグインは機能しない（root cause）

TypeScript がモジュールを解決する際、pnpm のシンボリックリンクを経由するため `isExternalLibraryImport: true` となる。

```json
{
  "resolvedFileName": "/path/to/packages/sub/dist/domain/domain-error.d.ts",
  "originalPath": "/path/to/apps/myapp/node_modules/@myorg/sub/dist/domain/domain-error.d.ts",
  "isExternalLibraryImport": true
}
```

`eslint-plugin-import-access` は `isExternalLibraryImport: true` のシンボルに対するチェックをスキップする。同一 TypeScript プロジェクト内のファイル間アクセス制御を目的としたプラグインであり、`node_modules` 経由のパッケージは対象外。

## 6. 結論

| レイヤー | 結果 |
|---------|------|
| TypeScript Language Service Plugin（エディタ） | 機能する（`.d.ts` に `@private` 付加）|
| ESLint プラグイン（`import-access/jsdoc`） | **機能しない**（`isExternalLibraryImport: true` のためスキップ）|

pnpm workspace 環境でクロスパッケージの import を ESLint で制御するには、別のアプローチが必要。
