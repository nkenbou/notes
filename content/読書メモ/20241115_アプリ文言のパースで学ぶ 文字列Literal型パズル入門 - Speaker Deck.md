---
title: "読書メモ: アプリ文言のパースで学ぶ 文字列Literal型パズル入門 - Speaker Deck"
created: 2024-11-15
modified: 2024-11-15
tags:
  - TypeScript
  - TypeScript-Literal型
  - Tips
URL: https://speakerdeck.com/sajikix/apuriwen-yan-nopasudexue-bu-wen-zi-lie-literalxing-pazururu-men
著者: "Saji (@sajikix\r)"
公開日: 2024-11-15
開始日:
終了日:
---
- **URL:** [アプリ文言のパースで学ぶ 文字列Literal型パズル入門 - Speaker Deck](https://speakerdeck.com/sajikix/apuriwen-yan-nopasudexue-bu-wen-zi-lie-literalxing-pazururu-men)
- **著者:** Saji (@sajikix
)
- **公開日:** 2024-11-15

## いつ読むか？

- TypeScript で Literal に型をつけたいとき
	- 文字列リテラルを扱うテクニック

## 読書メモ

### 概要

TypeScript のテンプレートリテラル型と `infer` を使って、文字列パターンから型を抽出するテクニック。

### 核心テクニック

- **テンプレートリテラル型 + infer**: `T extends \`${infer Before}.js\`` で ".js" の前の部分を型として取得
- **再帰型**: 複数のプレースホルダーを処理するために型定義内で自身を呼び出す

### ユースケース

i18n の翻訳文字列 `"Hello, {{name}}"` から `name` パラメータを自動抽出し、関数引数の型として強制する。

### 使いどころ

- 翻訳キーのプレースホルダー検証
- 文字列パターンの型安全なパーサー構築
- テンプレート文字列の引数型を自動推論したいとき
