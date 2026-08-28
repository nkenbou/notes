---
title: "react-to-web-component を使って React コンポーネントを Web Components に変換する"
created: 2024-10-20
modified: 2024-10-20
permalink: d6911bbb4448
tags:
  - react-to-web-component
  - React
  - WebComponents
URL: https://azukiazusa.dev/blog/react-to-web-component/
著者: azukiazusa (@azukiazusa9)
公開日: 2024-10-20
開始日:
終了日:
---
# 読書メモ: react-to-web-component を使って React コンポーネントを Web Components に変換する

- **URL:** [react-to-web-component を使って React コンポーネントを Web Components に変換する](https://azukiazusa.dev/blog/react-to-web-component/)
- **著者:** azukiazusa (@azukiazusa9)
- **公開日:** 2024-10-20

## いつ読むか？

- React でレンダリングした結果を Web Components にしたいとき

## 読書メモ

### 概要

`@r2wc/react-to-web-component` は React コンポーネントをカスタム要素 (Web Components) に変換するライブラリ。

### 基本的な使い方

```javascript
const HelloWorldComponent = r2wc(HelloWorld);
customElements.define("hello-world", HelloWorldComponent);
```

### 重要なポイント

- **Props の型指定**: `props` オプションで属性を指定。対応型は string / number / boolean / array / json / function
- **ケース変換**: キャメルケースは自動でケバブケースに変換される
- **関数型 Props**: グローバルスコープに関数を登録し、属性値として関数名を渡す
- **children の扱い**: 2つの方法がある
  - string 型で受け取る
  - `<slot>` 要素と shadow DOM を使う

### 活用場面

- フレームワーク非依存のコンポーネントライブラリ作成
- 既存の非 React プロジェクトへの React コンポーネント統合
- マイクロフロントエンドでの利用
