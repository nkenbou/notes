---
title: "Parse, don’t validate"
created: 2019-11-05
modified: 2019-11-05
permalink: c9c6d640bf98
tags:
  - プログラミング作法
  - 契約による設計
  - 型駆動設計
URL: https://lexi-lambda.github.io/blog/2019/11/05/parse-don-t-validate/
著者: "@lexi_lambda"
公開日: 2019-11-05
開始日:
終了日:
---
# 読書メモ: Parse, don’t validate

- **URL:** [Parse, don’t validate](https://lexi-lambda.github.io/blog/2019/11/05/parse-don-t-validate/)
- **著者:** @lexi_lambda
- **公開日:** 2019-11-05

## いつ読むか？

- 「Parse, don’t validate」の原典を参照したいとき
- バリデーション後の型を安全なものとして扱いたいとき

## 読書メモ

### 核心

**Validate は情報を捨てる、Parse は情報を型に残す**

- Validate: `[a] -> IO ()` → チェック後に知識が消える
- Parse: `[a] -> IO (NonEmpty a)` → 検証結果が型に埋め込まれる

### いつ使うか

- 外部入力 (JSON, CLI引数, DB) の境界処理
- 同じ条件を複数箇所でチェックしている時
- 不正状態がプログラム全体に波及しうる時

### 実践方法

1. **違法状態を表現不可能な型を選ぶ** - `NonEmpty a` など
2. **入力源から型を精密化する** - コンパイルエラーを呼び出し元に向かって追跡し修正
3. **型チェッカーに変更箇所を追跡させる**

### 例: head 関数

```haskell
-- 危険: 部分関数
head :: [a] -> a

-- 冗長: 毎回 Nothing チェックが必要
head :: [a] -> Maybe a

-- 最善: 型安全かつ冗長性なし
head :: NonEmpty a -> a
```
