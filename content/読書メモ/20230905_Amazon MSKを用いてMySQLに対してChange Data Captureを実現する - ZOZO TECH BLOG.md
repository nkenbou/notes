---
title: "Amazon MSKを用いてMySQLに対してChange Data Captureを実現する - ZOZO TECH BLOG"
created: 2023-09-05
modified: 2023-09-05
permalink: c007dd91e24f
tags:
  - EventSourcing
  - AmazonMSK
  - CDC
URL: https://techblog.zozo.com/entry/change-data-capture-for-mysql-using-amazon-msk
著者: "@ZOZO"
公開日: 2023-09-05
開始日:
終了日:
---
# 読書メモ: Amazon MSKを用いてMySQLに対してChange Data Captureを実現する - ZOZO TECH BLOG

- **URL:** [Amazon MSKを用いてMySQLに対してChange Data Captureを実現する - ZOZO TECH BLOG](https://techblog.zozo.com/entry/change-data-capture-for-mysql-using-amazon-msk)
- **著者:** @ZOZO
- **公開日:** 2023-09-05

## いつ読むか？

- Amazon MSK で CDC や Event Sourcing をやりたいとき

## 読書メモ

### 概要
ZOZOがマイクロサービス移行時に、配送サービスと基幹システム間の非同期データ同期をCDCで実現した事例。

### アーキテクチャ
- **Outboxパターン + Debezium** を採用
- Aurora MySQL → MSK Connect (Debezium) → Amazon MSK (Kafka) → Event Consumer

### 重要ポイント
- イベントは集約IDでパーティション分割（主キーではなく）→ 関連イベントの順序保証
- コンシューマはシーケンス番号で冪等性を担保
- MSK Connectの再デプロイは約15分かかる（完全再作成が必要）
- 例外処理は指数バックオフ（最大60秒）、失敗時はDBにログ

### 活用場面
- マイクロサービス間の非同期データ同期
- 下流サービス障害時も独立運用が必要な場合
- マネージドKafkaでイベント駆動アーキテクチャを構築する場合
