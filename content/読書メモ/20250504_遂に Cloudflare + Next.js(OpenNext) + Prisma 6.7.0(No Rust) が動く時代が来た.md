---
title: "遂に Cloudflare + Next.js(OpenNext) + Prisma 6.7.0(No Rust) が動く時代が来た"
created: 2025-05-04
modified: 2025-05-04
permalink: 6b1da5d318d7
tags:
  - Cloudflare
  - NextJS
  - Prisma
URL: https://zenn.dev/mizchi/articles/cloudflare-opennext-prisma-no-rust
著者: "@mizchi"
公開日: 2025-05-04
開始日:
終了日:
---
# 読書メモ: 遂に Cloudflare + Next.js(OpenNext) + Prisma 6.7.0(No Rust) が動く時代が来た

- **URL:** [遂に Cloudflare + Next.js(OpenNext) + Prisma 6.7.0(No Rust) が動く時代が来た](https://zenn.dev/mizchi/articles/cloudflare-opennext-prisma-no-rust)
- **著者:** @mizchi
- **公開日:** 2025-05-04

## いつ読むか？

- クラウド上に公開するアプリやサービスを開発するときの技術選定のとき

## 読書メモ


**何ができるか**: Cloudflare Workers 上で Next.js + Prisma が動く（ビルドサイズ 102KB）

**必要なもの**:
- OpenNext for Cloudflare
- Prisma 6.7.0（TypeScript版、Rustなし）
- prisma-postgres（無料枠あり）

**セットアップの流れ**:
1. `npm create cloudflare@latest -- my-app --framework=next --platform=workers`
2. Prisma の previewFeatures に `queryCompiler` と `driverAdapters` を設定
3. `npx prisma generate --no-engine` でエンジンなしビルド

**注意点**:
- プレビュー版のため本番利用は慎重に
- `"use cache"` 未対応
- D1（SQLite）、MySQL 非対応
- Vercel の新機能追従が遅れる可能性あり
