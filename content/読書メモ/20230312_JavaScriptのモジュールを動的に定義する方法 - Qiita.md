---
title: "読書メモ: JavaScriptのモジュールを動的に定義する方法 - Qiita"
created: 2023-03-12
modified: 2023-03-12
tags:
  - JavaScript
URL: https://qiita.com/suin/items/427d11ca9da397c52520
著者: "@suin"
公開日: 2023-03-12
開始日:
終了日:
---
- **URL:** [JavaScriptのモジュールを動的に定義する方法 - Qiita](https://qiita.com/suin/items/427d11ca9da397c52520)
- **著者:** @suin
- **公開日:** 2023-03-12

## いつ読むか？

- JavaScriptのモジュールを動的に定義したいとき

## 読書メモ

### 概要

文字列で定義した JavaScript コードを Data URL スキームで動的にモジュールとしてインポートする手法。

### コード例

```javascript
const code = `export default 1; export const a = 2;`;

function createModule(code) {
  return "data:text/javascript;charset=utf-8," + encodeURIComponent(code);
}

const module = await import(createModule(code));
// { a: 2, default: 1 }
```

### 使いどころ

- ランタイムで動的にコードを生成・実行したい場合
- 文字列からモジュールを作成したい場合

### 注意点

信頼できないコードの実行にはセキュリティリスクがある。
