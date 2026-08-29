---
title: "読書メモ: なぜ強調表示できず ** が表示されるのか — Perlで始まったMarkdownの歴史と日本語文書における課題 - Speaker Deck"
created: 2026-01-27
modified: 2026-01-27
tags:
  - Markdown
URL: https://speakerdeck.com/kwahiro/nazeqiang-diao-biao-shi-dekizu-star-star-gabiao-shi-sarerunoka-perldeshi-matutamarkdownnoli-shi-tori-ben-yu-wen-shu-niokeruke-ti
著者: kwahiro (hkws)
公開日: 2025-11-13
開始日: 2026-01-27
終了日: 2026-01-27
---
- **URL:** [なぜ強調表示できず ** が表示されるのか — Perlで始まったMarkdownの歴史と日本語文書における課題 - Speaker Deck](https://speakerdeck.com/kwahiro/nazeqiang-diao-biao-shi-dekizu-star-star-gabiao-shi-sarerunoka-perldeshi-matutamarkdownnoli-shi-tori-ben-yu-wen-shu-niokeruke-ti)
- **著者:** kwahiro (hkws)
- **公開日:** 2025-11-13

## いつ読むか？

- Markdown で `**強調**` が正しく表示されない事象を説明するとき

## 読書メモ

### なぜ日本語だと強調表示に失敗するのか

分かち書き（語の区切りに空白を挟んで記述すること）をしない言語は、以下のルールが自然に満たされない：

- 強調開始時：`**` の直後が約物で、`**` の直前が空白または約物
- 強調終了時：`**` の直前が約物で、`**` の直後が空白または約物

### 対策

- CJK 対応パーサーを使う（Comrak、remark-cjk-friendly など）
- 空白 → マーカー → 約物の順で書く
