---
title: "読書メモ: TypeScript による GraphQL バックエンド開発 - Speaker Deck"
created: 2022-10-14
modified: 2022-10-14
permalink: f50c15b97503
tags:
  - TypeScript
  - BrandedTypes
URL: https://speakerdeck.com/naoya/typescript-niyoru-graphql-batukuendokai-fa-75b3dab7-90a8-4169-a4dc-d1e7410b9dbd?slide=91
著者: 伊藤直也 (@naoya_ito)
公開日: 2022-10-14
開始日:
終了日:
---
- **URL:** [TypeScript による GraphQL バックエンド開発 - Speaker Deck](https://speakerdeck.com/naoya/typescript-niyoru-graphql-batukuendokai-fa-75b3dab7-90a8-4169-a4dc-d1e7410b9dbd?slide=91)
- **著者:** 伊藤直也 (@naoya_ito)
- **公開日:** 2022-10-14

## いつ読むか？

- Branded Types のリファレンス実装として

## 読書メモ

### 概要

フロントエンドの状態管理パラダイム（Elm アーキテクチャ）をバックエンド開発に適用する手法の提案。

### 主要技術

- **Result 型**: `neverthrow` ライブラリで計算失敗を型で表現。`andThen()` でエラーハンドリングを統合
- **Tagged Union 型**: ドメインモデルの状態遷移（Unvalidated → Validated → Created）を型安全に表現
- **ワークフローパターン**: ビジネスロジックを純粋関数として分離し、DI で I/O を外部化

### 実践のポイント

- クラスより小さな関数と型による宣言的設計
- ドメインロジックとデータ永続化を明確に分離
- 例外スローを最小化し Result 型で結果を扱う
