---
title: "読書メモ: Skills | j5ik2o/okite-ai"
created: 2026-05-20
modified: 2026-05-20
permalink: dfd33499b5be
tags:
  - DDD
  - ソフトウェア設計
  - ベストプラクティス
URL: https://github.com/j5ik2o/okite-ai/blob/main/docs/skills.md
著者: j5ik2o
公開日: 
開始日: 2026-05-20
終了日: 2026-05-20
---
- **URL:** [okite-ai/docs/skills.md at main · j5ik2o/okite-ai](https://github.com/j5ik2o/okite-ai/blob/main/docs/skills.md)
- **著者:** j5ik2o
- **公開日:** 

## いつ読むか？

- ソフトウェア設計の判断に迷ったとき、業界のベストプラクティスを確認したいとき
- DDD や CQRS/ESの 導入・設計をレビューするとき
- 設計の相談相手として信頼できる著者の見解をまとめて参照したいとき

## 読書メモ

業界で語られてきたソフトウェア設計のベストプラクティスをカタログ形式でまとめたドキュメント。著者は各トピックの実装サンプルを用意しており、概念の説明にとどまらず実践的な参照資料として機能する。

### DDD / Domain Modeling

- **`aggregate-design`** — 集約設計ルールに基づく設計・レビュー。どこで境界を引くかの指針
- **`aggregate-transaction-boundary`** — 集約とトランザクション境界の関係。1トランザクション＝1集約の原則を整理
- **`cross-aggregate-constraints`** — 集約をまたぐ制約をどう設計するか。結果整合・ドメインサービスの使い分け
- **`domain-building-blocks`** — 値オブジェクト・エンティティ・集約・ドメインサービスの選択基準
- **`domain-model-first`** — コードより先にドメインモデルを設計する開発手順
- **`domain-model-extractor`** — 既存コードからドメインモデルを抽出する手法
- **`domain-primitives-and-always-valid`** — Domain Primitives パターンと「常に有効な状態」の設計
- **`ddd-module-pattern`** — DDDのモジュールパターンに沿ったパッケージ構造設計
- **`repository-design`** — リポジトリ設計のルールとアンチパターン
- **`repository-placement`** — リポジトリをどのレイヤーに置くべきかのガイド
- **`when-to-wrap-primitives`** — プリミティブ型を値オブジェクトでラップすべきか否かの判断基準

### CQRS / Event Sourcing

- **`cqrs-aggregate-modeling`** — CQRS/ES導入時の集約モデリング。コマンド側とクエリ側の分離方針
- **`cqrs-to-event-sourcing`** — CQRSがEvent Sourcingを必要とする背景と経緯の整理
- **`cqrs-tradeoffs`** — CQRSにおける一貫性・可用性・拡張性のトレードオフ分析
- **`pekko-cqrs-es-implementation`** — Scala 3 + Pekko（旧Akka）でのCQRS/ES実装パターン

### Architecture / Design

- **`clean-architecture`** — クリーンアーキテクチャの設計・レビュー支援。依存の方向の原則
- **`error-classification`** — Error / Defect / Fault / Failure の分類と使い分け
- **`error-handling`** — 回復可能性を基準としたエラー設計（回復可能・不可能の分類）
- **`parse-dont-validate`** — 「検証するな、パースせよ」パターン。型で不正状態を表現不可能にする
- **`backward-compat-governance`** — 後方互換性のガバナンス設計。破壊的変更をどう管理するか

### OOP Principles

- **`tell-dont-ask`** — オブジェクトに状態を問い合わせて処理するのでなく、命令する設計
- **`law-of-demeter`** — デメテルの法則（最小知識の原則）に基づく結合度の改善
- **`first-class-collection`** — コレクションを専用クラスで包む設計。ドメイン知識のカプセル化
- **`breach-encapsulation-naming`** — カプセル化を暗黙に壊すgetterの命名規約の問題
- **`intent-based-dedup`** — 「意図が同じか」を基準に共通化を判断する手法（機械的なDRYの回避）

### Package / Module Refactoring

- **`package-design`** — パッケージ・モジュール構造の設計指針
- **`refactoring-packages`** — 既存構造を分割・整理するリファクタリング手法
