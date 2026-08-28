---
title: "読書メモ: Ports & Adapters パターン：Hexagonal Architecture Explained を手元に"
created: 2025-10-04
modified: 2025-10-04
permalink: fdc057ff5315
tags:
  - PortsAndAdapters
  - アーキテクチャー
URL: https://zenn.dev/kkatou/articles/ports-and-adapters-explained
著者: KKatou7209
公開日: 2025-10-04
開始日:
終了日:
---
- **URL:** [Ports & Adapters パターン：Hexagonal Architecture Explained を手元に](https://zenn.dev/kkatou/articles/ports-and-adapters-explained)
- **著者:** KKatou7209
- **公開日:** 2025-10-04

## いつ読むか？

- ポートアンドアダプターのキャッチアップをしたいとき
- リファレンス実装
- ポートアンドアダプターの参考文献を探したいとき

## 読書メモ

### 核心概念

アプリケーションを中心に、外部との接点を Port と Adapter で仲介する。

- **Port**: アプリと外部の接合部（インターフェース）
  - Driving Port: 外部からアプリを利用（UI、API）
  - Driven Port: アプリが外部を利用（DB、外部サービス）
- **Adapter**: Port と実装の間で仕様差を吸収
- **Configulater**: 依存関係を解決し、具体実装を接続

### 実装の流れ

1. Port（インターフェース）を先に定義
2. アプリケーション層は Port にのみ依存
3. DB・UI 等の具体実装は Adapter で隔離
4. Configulater で全体を統合

### 向き不向き

- 向いている: 中〜大規模、継続的拡張予定のシステム
- 避けるべき: 小規模、プロトタイプ段階

### トレードオフ

メリット: 可搬性、拡張性、テスト容易性、分担開発の効率化
デメリット: 習得難度、過度な複雑性リスク、処理フロー追跡の困難さ
