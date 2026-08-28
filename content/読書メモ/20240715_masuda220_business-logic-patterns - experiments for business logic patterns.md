---
permalink: d14623f19d77
tags:
  - DDD
  - オブジェクト指向
  - ドメインモデル実装
URL: https://github.com/masuda220/business-logic-patterns
著者: 増田亨 (@masuda220)
公開日: 2024-07-15
開始日:
終了日:
---
# 読書メモ: Business Logic Patterns

- **URL:** [Business Logic Patterns](https://github.com/masuda220/business-logic-patterns)
- **著者:** 増田亨 (@masuda220)
- **公開日:** 2024-07-15

## いつ読むか？

- ドメインモデルのリファレンス実装を探しているとき

## 読書メモ

### 何のリポジトリか

業務アプリケーションのドメインオブジェクト設計パターン集（Java）。再利用部品ではなく学習教材。

### 核心の問題意識

`BigDecimal` や `LocalDate` は汎用的すぎて業務には使いづらい：
- 値の範囲が広すぎる
- 不要なメソッドが多い / 必要なメソッドがない

### 解決策

**特定の文脈・用途に最適化されたシンプルな値クラス**を作る。

### パターンの対象領域

- 数量と単位
- 金額（計算、税、割引）
- 日付（計算、日数）
- 範囲（from-to）
- 状態遷移

### いつ使うか

- 値オブジェクト設計時の参考に
- 「この業務概念をどう型にするか」迷ったときに
