---
title: "Introduction to Event Sourcing | Kurrent"
created: 2025-11-23
modified: 2025-11-23
permalink: 553a5b6df15c
tags:
  - EventSourcing
  - CQRS
URL: https://www.kurrent.io/event-sourcing
著者: "@Kurrent"
公開日:
開始日: 2025-11-23
終了日:
---
# 読書メモ: Introduction to Event Sourcing | Kurrent

- **URL:** [Introduction to Event Sourcing | Kurrent](https://www.kurrent.io/event-sourcing)
- **著者:** @Kurrent

## いつ読むか？

- Event Sorcing の概要と実例を包括的に学びたいとき

## 読書メモ

### Event Sourcing とは

アプリケーションの全ての変化をドメインイベントとして append-only で記録するアーキテクチャパターン。

### 使いどころ

- **監査要件が厳しい業務**: 全履歴が残るため完全な監査ログが得られる
- **モノリスの分解**: ビジネスロジックとデータモデルを分離し、マイクロサービス化を支援
- **分析・AI 活用**: 過去の状態復元や時系列分析、AI トレーニングデータの生成

### 基本の流れ

1. ドメインイベントを記録（追記のみ）
2. イベントをリプレイしてプロジェクションを構築
3. 用途に最適化したデータモデルを作成

### 従来手法との違い

通常の DB は更新時に履歴を上書きするが、Event Sourcing は全履歴を永続保存する。
