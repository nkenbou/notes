---
permalink: 09c758b6dd29
tags:
  - EventSourcing
  - データモデリング
URL: https://aws.amazon.com/jp/blogs/news/build-a-cqrs-event-store-with-amazon-dynamodb/
著者: "@AWS"
公開日: 2022-10-31
開始日:
終了日:
---
# 読書メモ: Amazon DynamoDB を使った CQRS イベントストアの構築 | Amazon Web Services ブログ

- **URL:** [Amazon DynamoDB を使った CQRS イベントストアの構築 | Amazon Web Services ブログ](https://aws.amazon.com/jp/blogs/news/build-a-cqrs-event-store-with-amazon-dynamodb/)
- **著者:** @AWS
- **公開日:** 2022-10-31

## いつ読むか？

- Event Sourcing のストレージのスキーマ例として

## 読書メモ

### 概要

DynamoDB を使ってイベントソーシングのイベントストアを構築する方法を解説。CQRS パターンと組み合わせた実装例を紹介。

### テーブル設計

- **パーティションキー**: 集約 ID（aggregate_id）
- **ソートキー**: シーケンス番号（sequence_number）
- 1 つの集約に対するイベントを時系列順で格納

### 楽観的ロック

- `ConditionExpression` を使用
- `attribute_not_exists(sequence_number)` で重複を防止
- 同時書き込み時は `ConditionalCheckFailedException` をキャッチしてリトライ

### イベント読み取り

- `Query` で集約 ID を指定し、全イベントを取得
- ソートキーで自動的に順序保証
- スナップショットと組み合わせてパフォーマンス向上

### 実践ポイント

- GSI でイベントタイプ別のクエリを可能に
- DynamoDB Streams で他システムへのイベント配信
- TTL でイベントのアーカイブ・削除を管理
