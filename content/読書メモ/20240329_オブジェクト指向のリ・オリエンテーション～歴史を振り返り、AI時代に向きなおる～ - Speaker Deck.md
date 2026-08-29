---
title: "読書メモ: オブジェクト指向のリ・オリエンテーション～歴史を振り返り、AI時代に向きなおる～ - Speaker Deck"
created: 2024-03-29
modified: 2024-03-29
tags:
  - オブジェクト指向
  - ドメインモデリング
  - DDD
URL: https://speakerdeck.com/hanyudaeiiti/obuziekutozhi-xiang-noriorientesiyon-li-shi-wozhen-rifan-ri-aishi-dai-nixiang-kinaoru?slide=31
著者: 羽生田栄一 (@HHany)
公開日: 2024-03-29
開始日:
終了日:
---
- **URL:** [オブジェクト指向のリ・オリエンテーション～歴史を振り返り、AI時代に向きなおる～ - Speaker Deck](https://speakerdeck.com/hanyudaeiiti/obuziekutozhi-xiang-noriorientesiyon-li-shi-wozhen-rifan-ri-aishi-dai-nixiang-kinaoru?slide=31)
- **著者:** 羽生田栄一 (@HHany)
- **公開日:** 2024-03-29

## いつ読むか？

- オブジェクト指向の歴史をふりかえりたいとき (2024年3月29日時点)
- OOA、OOD などのコンテキストでのオブジェクト指向をキャッチアップしたい

## 読書メモ

### 核心メッセージ

OOPの本質は「メッセージングによる抽象化と処理の遅延」であり、クラスや継承ではない。

### OOP進化の5段階

1. メッセージング、低結合度
2. 責務・ロール整理（SRP）
3. クラス・継承・多相 ← **形式的な意味なし、迅速に通過すべき**
4. 構造主義的OO（OCP+LSP、SOLID原則）
5. DDD基本（パッケージ設計、関心分離）

### 実践上の注意点

- Getter/Setterは真の抽象データ型ではない
- **Liskovの置換原則を理解せずに継承を使うべきではない**
- モデリングは「モノ（管理対象）・コト（イベント）・バ（場所）」で分類

### AI時代への示唆

自然言語プログラミングの時代において、「対象に良い名前を付け、希望を伝える（メッセージング）」という思考法が重要になる。
