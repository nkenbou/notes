---
title: "読書メモ: いまさら聞けない CSS の「Shorthand」と「Longhand」って何が違うの？"
created: 2026-08-06
modified: 2026-08-06
tags:
  - CSS
  - フロントエンド
URL: https://blog.sakupi01.com/dev/articles/demystify-css-shorthand-longhand-properties
著者: saku (@sakupi01)
公開日: 2026-07-28
開始日: 2026-08-06
終了日: 2026-08-06
---
- **URL:** [いまさら聞けない CSS の「Shorthand」と「Longhand」って何が違うの？](https://blog.sakupi01.com/dev/articles/demystify-css-shorthand-longhand-properties)
- **著者:** saku (@sakupi01)
- **公開日:** 2026-07-28

## いつ読むか？

- `background` や `border` などのショートハンドとロングハンドのどちらで書くか迷ったとき
- 既存コンポーネントのスタイルを一部だけ調整したいのに、意図せず他の見た目まで変わってしまったとき
- ショートハンドの後に書いたロングハンドが効かない / 効きすぎる理由を知りたいとき
- CSS の書き方を lint ルールで機械的に統一しようとしているとき

## 読書メモ

**選択基準はデザインの意図**。関連プロパティをまとめて初期化する「完全に上書きするデザイン」ならショートハンド、既存を維持して「一部だけ変更するデザイン」ならロングハンド。

- ショートハンドには初期値がなく、必ずロングハンドに展開される。**明示しなかったサブプロパティは初期化される** (`border` を書くと `border-image` は必ずリセット)
- 展開は**カスケードより前**に起こる。だから後続の指定との前後関係が直感とずれる
- `inherit` や `!important` は展開先の全ロングハンドに伝播する

lint の静的ルールでは判断しきれない領域。
