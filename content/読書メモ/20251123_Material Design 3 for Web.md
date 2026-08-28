---
title: "読書メモ: Material Design 3 for Web"
created: 2025-11-23
modified: 2025-11-23
permalink: a67224fd66da
tags:
  - WebComponents
  - MaterialDesign
URL: https://m3.material.io/develop/web
著者: "@Google"
公開日:
開始日: 2025-11-23
終了日:
---
- **URL:** [Material Design 3 for Web](https://m3.material.io/develop/web)
- **著者:** @Google

## いつ読むか？

- Web Components のリファレンス実装として

## 読書メモ

### Material Web Components (MWC) とは

- Google が提供する Material Design 3 準拠の Web Components ライブラリ
- Lit, React, Vue, Svelte など多くのフレームワークで動作
- CSS カスタムプロパティによるデザイントークンで統一スタイリング

### 使いどころ

- `<button>`, `<input>` などの標準要素を Material Design スタイルに置き換えたいとき
- フレームワーク非依存で Material Design 3 を導入したいとき

### 重要な注意点（2024年6月〜）

**MWC はメンテナンスモードに移行**
- Google 社内の Wiz フレームワーク対応に注力するため、開発が停止
- Card, Navigation Drawer などの計画されていたコンポーネントは未実装のまま
- 新規プロジェクトでの採用は要検討

### 代替手段

- **Angular Material**: Angular チームがフォークして開発継続
- **Beer CSS**: 軽量な Material Design 3 代替
- **コミュニティフォーク**: 各種派生プロジェクト
