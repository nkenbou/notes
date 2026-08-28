---
permalink: 31bdf56a9a9e
tags:
  - DDD
  - EventSourcing
  - CQRS
URL: https://www.dondakeshimo.com/posts/2024-05-06-domain-event-design
著者: 下村拓 (@dondakeshimo)
公開日: 2024-05-11
開始日:
終了日:
---
# 読書メモ: Domain Event | dondakeshimoの丸太

- **URL:** [Domain Event | dondakeshimoの丸太](https://www.dondakeshimo.com/posts/2024-05-06-domain-event-design)
- **著者:** 下村拓 (@dondakeshimo)
- **公開日:** 2024-05-11

## いつ読むか？

- ドメインイベントの概要から実践まで包括的に理解したいとき

## 読書メモ

### Domain Eventとは
- ドメイン専門家が関心を持つ「過去に起きた出来事」を表現するモデル
- Aggregateによって発行される

### 3つの実装パターン
1. **静的Publisherパターン**: Aggregateが直接通知。シンプルだが副作用が強い
2. **戻り値パターン**: Commandの返り値としてイベントを返す。処理順序を制御可能
3. **保持パターン**: Aggregateが内部にイベントを保持。クライアント責務を軽減

### 設計の原則
- **不変性**: 過去の出来事なので変更不可
- **独立性**: 1つの出来事を1つのイベントで表現
- **完全な情報**: 復元に必要な全情報を含める
- **バージョニング**: スキーマ進化を考慮

### 実践的なポイント
- フレームワークに依存せずコアドメインとして実装
- Outboxパターンで永続化と外部通知の整合性を担保
