---
title: "EventStoreが利用するDynamoDBのテーブル構成"
created: 2023-09-18
modified: 2023-09-18
permalink: 1ca321c3e9db
tags:
  - EventSourcing
  - データモデリング
URL: https://github.com/j5ik2o/event-store-adapter-js/blob/main/docs/DATABASE_SCHEMA.ja.md
著者: "加藤潤一 (\r@j5ik2o)"
公開日: 2023-09-18
開始日:
終了日:
---
# 読書メモ: EventStoreが利用するDynamoDBのテーブル構成

- **URL:** [EventStoreが利用するDynamoDBのテーブル構成](https://github.com/j5ik2o/event-store-adapter-js/blob/main/docs/DATABASE_SCHEMA.ja.md)
- **著者:** 加藤潤一 (
@j5ik2o)
- **公開日:** 2023-09-18

## いつ読むか？

- Event Sourcing のストレージのスキーマ例として

## 読書メモ

### 概要
DynamoDBでイベントソーシングを実現するための2テーブル構成（Journal + Snapshot）

### Journalテーブル
- イベントを時系列で保存
- pkey: `集約種別名-hash(集約ID) % シャードサイズ` で分散書き込み
- skey: `集約種別名-集約ID-シーケンス番号`

### Snapshotテーブル
- 集約の状態を保存してリプレイを高速化
- skey=0 に最新スナップショットを保持
- `version` 属性で楽観的ロック

### 重要ポイント
- JournalとSnapshotは同一トランザクションで書き込み
- スナップショット以降のイベントを適用して最新状態を復元
