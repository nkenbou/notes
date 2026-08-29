---
title: "読書メモ: HTML だけで Shadow DOM を構築するための宣言型 Shadow DOM"
created: 2024-10-19
modified: 2024-10-19
tags:
  - ShadowDOM
  - WebComponents
URL: https://azukiazusa.dev/blog/declarative-shadow-dom/
著者: azukiazusa (@azukiazusa9)
公開日: 2024-10-19
開始日:
終了日:
---
- **URL:** [HTML だけで Shadow DOM を構築するための宣言型 Shadow DOM](https://azukiazusa.dev/blog/declarative-shadow-dom/)
- **著者:** azukiazusa (@azukiazusa9)
- **公開日:** 2024-10-19

## いつ読むか？

- Web Components を始めたい
- Shadow DOM をキャッチアップしたい

## 読書メモ

### 要点

- 宣言型 Shadow DOM は `<template shadowrootmode="open">` を使い、JavaScript なしで Shadow DOM を構築できる
- SSR 対応が可能になり、初期表示の高速化と SEO 改善に寄与

### 使い方

```html
<my-component>
  <template shadowrootmode="open">
    <style>p { color: red; }</style>
    <p>コンテンツ</p>
  </template>
</my-component>
```

### 実践ポイント

- SSR でコンポーネントを出力し、後から JS で動的機能を追加するパターンに有効
- JS から生成する場合は `innerHTML` ではなく `setHTMLUnsafe()` を使用（XSS に注意）
