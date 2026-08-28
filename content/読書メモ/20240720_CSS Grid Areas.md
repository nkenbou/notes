---
title: "CSS Grid Areas"
created: 2024-07-20
modified: 2024-07-20
permalink: 14de50a97b9a
tags:
  - CSS
  - CSSGrid
URL: https://ishadeed.com/article/css-grid-area/
著者: "@shadeed9"
公開日:
開始日:
終了日:
---
# 読書メモ: CSS Grid Areas

- **URL:** [CSS Grid Areas](https://ishadeed.com/article/css-grid-area/)
- **著者:** @shadeed9

## いつ読むか？

- CSS のグリッドレイアウトをキャッチアップしたいとき

## 読書メモ

### 要点

- `grid-template-areas` で領域に名前をつけ、`grid-area` で配置する手法
- レイアウト構造が CSS 上で視覚的にわかる
- レスポンシブ対応時、親の `grid-template-areas` を書き換えるだけで子要素の変更不要

### 使いどころ

- ヘッダーのロゴ・ナビ・アクションをビューポートごとに再配置
- カードの画像・タイトル・本文の順序を柔軟に変更
- 同一コンポーネントで複数レイアウトバリエーションを持たせたいとき

### 注意点

- 領域は長方形である必要がある
- 空セルはドット (`.`) で定義
- 長方形以外の複雑な配置には named grid lines を使う
