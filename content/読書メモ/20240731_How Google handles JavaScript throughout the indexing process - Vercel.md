---
title: "読書メモ: How Google handles JavaScript throughout the indexing process - Vercel"
created: 2024-07-31
modified: 2024-07-31
tags:
  - Googleクローラー
  - SEO
URL: https://vercel.com/blog/how-google-handles-javascript-throughout-the-indexing-process
著者: "@Vercel"
公開日: 2024-07-31
開始日:
終了日:
---
- **URL:** [How Google handles JavaScript throughout the indexing process - Vercel](https://vercel.com/blog/how-google-handles-javascript-throughout-the-indexing-process)
- **著者:** @Vercel
- **公開日:** 2024-07-31

## いつ読むか？

- Google のクローラーでは JavaScript のレンダリングがされることを伝えるときの証左を示したいとき

## 読書メモ

### 要点

GoogleはJavaScriptを問題なくレンダリング・インデックスできる。

### 検証結果

- 100,000回のGooglebotフェッチで100%レンダリング成功
- API経由の非同期コンテンツも完全にインデックス
- React Server Componentsのストリーミングも対応

### レンダリング時間

- 中央値: 10秒
- 75パーセンタイル: 26秒
- 90パーセンタイル: 約3時間

### 注意点

- `noindex`タグがHTMLにあるとレンダリングされない（JSで削除しても無効）
- クエリ文字列付きURLはレンダリングが遅延する傾向

### 実践時のポイント

- JSフレームワークは使って良いがパフォーマンスを重視
- 重要なSEO要素はSSRで出力
- robots.txtで重要リソースをブロックしない
- sitemap.xmlを定期的に更新
