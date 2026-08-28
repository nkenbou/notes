---
title: "TypeScript におけるモジュール関連オプションの整理. TypeScript 4.7 で “module” という名前で始まる… | by Yosuke Kurami | Medium"
created: 2022-05-09
modified: 2022-05-09
permalink: dd82529b741c
tags:
  - TypeScript
URL: https://quramy.medium.com/typescript-%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E9%96%A2%E9%80%A3%E3%82%AA%E3%83%97%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E6%95%B4%E7%90%86-efdf860a7c4
著者: "@Quramy"
公開日: 2022-05-09
開始日:
終了日:
---
# 読書メモ: TypeScript におけるモジュール関連オプションの整理. TypeScript 4.7 で “module” という名前で始まる… | by Yosuke Kurami | Medium

- **URL:** [TypeScript におけるモジュール関連オプションの整理. TypeScript 4.7 で “module” という名前で始まる… | by Yosuke Kurami | Medium](https://quramy.medium.com/typescript-%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E9%96%A2%E9%80%A3%E3%82%AA%E3%83%97%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E6%95%B4%E7%90%86-efdf860a7c4)
- **著者:** @Quramy
- **公開日:** 2022-05-09

## いつ読むか？

## 読書メモ

- TypeScript のモジュール関連オプション ("module" から始まる) を理解したいとき

### 核心ポイント

**import 指定子（`"./hoge"` の部分）はコンパイル時に書き換えられない**

### いつ使う？

- `.mts`/`.cts` ファイルで `import "./foo.cjs"` と拡張子付きで書く理由を知りたいとき
- `--moduleSuffixes` の挙動が理解できないとき
- `module`, `moduleResolution` などのオプションの違いを整理したいとき

### 覚えておくこと

TypeScript は import パスを変換しない → 出力先の実行環境が解決できるパスを書く必要がある
