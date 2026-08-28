---
permalink: d708fe348cba
tags:
  - DDD
  - ドメインモデリング
  - 関数型DDD
  - 集約
URL: https://github.com/kawasima/revisiting-domain-model
著者: 川島義隆 (@kawasima)
公開日: 2023-01-23
開始日:
終了日:
---
# 読書メモ: Revisiting Domain Model

- **URL:** [Revisiting Domain Model](https://github.com/kawasima/revisiting-domain-model)
- **著者:** 川島義隆 (@kawasima)
- **公開日:** 2023-01-23

## いつ読むか？

- ドメインモデリングについてより深く考えたいとき

## 読書メモ

### ドメインモデル設計のトリレンマ

ドメインモデル設計には3つの目標があり、同時にすべてを満たすことはできない：

1. **純粋性 (Purity)** - ドメインロジックの分離
2. **完全性 (Completeness)** - 集約の整合性
3. **パフォーマンス (Performance)** - 実行効率

### 設計パターンの選択肢

- **純粋性 + 完全性**: パフォーマンスを犠牲にする
- **パフォーマンス + 完全性**: 純粋性を犠牲にする
- **パフォーマンス + 純粋性**: 完全性を犠牲にする

### 解決アプローチ

- **集約の分割**: 集約を小さく分解してバランスを改善
- **関数型DDD**: 「Domain Modeling Made Functional」の手法を適用

### 実践への示唆

ドメインモデル設計時に「何を犠牲にするか」を明確に選択する必要がある。トレードオフを理解した上で、プロジェクトの要件に合った設計を選ぶ。
