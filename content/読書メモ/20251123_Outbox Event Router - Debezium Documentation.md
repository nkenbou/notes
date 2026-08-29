---
title: "読書メモ: Outbox Event Router :: Debezium Documentation"
created: 2025-11-23
modified: 2025-11-23
tags:
  - EventSourcing
  - Debezium
URL: https://debezium.io/documentation/reference/stable/transformations/outbox-event-router.html#emitting-messages-with-additional-fields
著者: "@Debezium"
公開日:
開始日: 2025-11-23
終了日:
---
- **URL:** [Outbox Event Router :: Debezium Documentation](https://debezium.io/documentation/reference/stable/transformations/outbox-event-router.html#emitting-messages-with-additional-fields)
- **著者:** @Debezium

## いつ読むか？

## 読書メモ

- Debezium で Outbox パターンをするときのドキュメント (Outbox Event Router)
- Event Sourcing のストレージのスキーマ例として

### 概要

Outbox Event RouterはDebeziumのSMT（Single Message Transformation）で、マイクロサービス間のデータ交換における整合性問題を解決する。

### 解決する問題

- サービスの内部状態（DB）と外部公開イベントの不整合を防ぐ
- DBへの書き込みとイベント発行を同一トランザクションで実現

### 仕組み

1. サービスがビジネスデータと同時にアウトボックステーブルにINSERT
2. Debeziumがアウトボックステーブルの変更をキャプチャ
3. Event RouterがKafkaトピックへの構造化イベントに変換

### アウトボックステーブルの基本構造

| カラム | 用途 |
|--------|------|
| id | イベントID（ヘッダー用） |
| aggregatetype | トピック名の決定（例：orders） |
| aggregateid | パーティションキー |
| payload | イベント本体（JSON） |

### 主要設定

- `route.by.field`: トピック名の基準カラム
- `route.topic.replacement`: トピック名テンプレート
- `table.expand.json.payload`: JSONペイロードの展開

### いつ使うか

- マイクロサービス間でイベント駆動アーキテクチャを構築するとき
- DBの更新とKafkaへのイベント発行のアトミック性が必要なとき
- Transactional Outboxパターンを実装するとき
