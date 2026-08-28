---
permalink: d2cf8ecf3496
tags:
  - DCI
  - DDD
URL: https://digitalsoul.hatenadiary.org/entry/20100131/1264925022
著者: "@digitalsoul0124"
公開日: 2010-01-31
開始日:
終了日:
---
# 読書メモ: DCI アーキテクチャ - Trygve Reenskaug and James O. Coplien - Digital Romanticism

- **URL:** [DCI アーキテクチャ - Trygve Reenskaug and James O. Coplien - Digital Romanticism](https://digitalsoul.hatenadiary.org/entry/20100131/1264925022)
- **著者:** @digitalsoul0124
- **公開日:** 2010-01-31

## いつ読むか？

- DCI アーキテクチャーの信頼できる参考文献を探しているとき

## 読書メモ

### 一言でいうと

オブジェクト指向の「構造」だけでなく「動作」も明確にするアーキテクチャ

### DCI の3要素

- **Data**: ドメインオブジェクトの安定した情報（口座の残高など）
- **Context**: ユースケース実行時にオブジェクトとロールを結びつける
- **Interaction**: ロール間の協調動作（振込元 → 振込先など）

### いつ使うか

- ユースケースの「振る舞い」がコードから読み取れない時
- ドメインモデルが肥大化してきた時
- エンドユーザのメンタルモデルとコードを直結させたい時
