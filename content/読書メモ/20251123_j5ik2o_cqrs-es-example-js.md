---
permalink: f5c5a9c3bcb5
tags:
URL: https://github.com/j5ik2o/cqrs-es-example-js
著者: "加藤潤一 (\r@j5ik2o)"
公開日:
開始日: 2025-11-23
終了日:
---
# 読書メモ: j5ik2o/cqrs-es-example-js

- **URL:** [j5ik2o/cqrs-es-example-js](https://github.com/j5ik2o/cqrs-es-example-js)
- **著者:** 加藤潤一 (
@j5ik2o)

## いつ読むか？

- Node.js + TypeScript のフルスタックアプリケーションのリファレンス実装として
- pnpm のモノレポのリファレンス実装として
- CQRS/イベントソーシングをTypeScriptで実装したい時
- GraphQL APIでCQRS構成を作りたい時
- イベントストアと読み取りモデルの連携パターンを学びたい時

## 読書メモ

### 概要

TypeScriptによるCQRS/イベントソーシングの実装例。クラスベース（非アクターモデル）。

### アーキテクチャ

```
書き込みサーバー → イベントストア → 読み取りモデル更新 → 読み取りサーバー
```

- 書き込み: GraphQL Mutation
- 読み取り: GraphQL Query

### 技術スタック

- Apollo Server + TypeGraphQL
- Prisma（ORM）
- event-store-adapter-js

### ポイント

- pnpmワークスペース + Turboでモノレポ管理
- Docker Compose対応
- 実践的なリファレンス実装として有用
