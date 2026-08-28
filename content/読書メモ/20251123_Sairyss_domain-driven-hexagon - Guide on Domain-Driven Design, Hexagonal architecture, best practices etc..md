---
title: "Domain-Driven Hexagon"
created: 2025-11-23
modified: 2025-11-23
permalink: 3ca5843fab1f
tags:
  - PortsAndAdapters
URL: https://github.com/Sairyss/domain-driven-hexagon
著者: "@Sairyss"
公開日:
開始日: 2025-11-23
終了日:
---
# 読書メモ: # Domain-Driven Hexagon

- **URL:** [# Domain-Driven Hexagon](https://github.com/Sairyss/domain-driven-hexagon)
- **著者:** @Sairyss

## いつ読むか？

- ポートアンドアダプターのリファレンス実装として

## 読書メモ

### 対象プロジェクト

複雑なビジネスロジックを持つ大規模プロジェクト向け。シンプルな CRUD には過度な抽象化。

### コアパターン

- **CQS**: Command（状態変更）と Query（読取）を分離
- **Aggregate**: ルートエンティティを通じた一貫性境界。外部からはルートのみ参照
- **Domain Event**: Aggregate 間は直接呼び出しではなくイベントで疎結合化

### プロジェクト構造

```
Application Core:
  - Domain Layer (Entities, Aggregates, Domain Services)
  - Application Layer (Use Cases, Commands/Queries, Ports)

外側:
  - Interface Adapters (Controllers, DTOs)
  - Infrastructure (Repositories, External Adapters)
```

モジュールは「垂直スライス」で整理。モジュール間は Facade/Mediator 経由で通信。

### 重要な設計原則

- **依存性の方向**: 常に内側（Domain）を指す
- **Port**: インフラ依存を抽象化。テスト時のモック化が容易
- **Entity**: コンストラクタで検証、意図的なメソッド名を使用（getter/setter より）
