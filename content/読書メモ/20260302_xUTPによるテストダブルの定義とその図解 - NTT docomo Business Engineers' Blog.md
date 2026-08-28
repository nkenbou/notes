---
title: "xUTPによるテストダブルの定義とその図解 - NTT docomo Business Engineers' Blog"
created: 2026-03-02
modified: 2026-03-02
permalink: 84c428e8cc44
tags:
  - TDD
  - テストダブル
URL: https://engineers.ntt.com/entry/20251208_advent-calendar-day8/entry
著者:
公開日: 2025-12-08
開始日: 2026-03-02
終了日: 2026-03-02
---
# 読書メモ: xUTPによるテストダブルの定義とその図解 - NTT docomo Business Engineers' Blog

- **URL:** [xUTPによるテストダブルの定義とその図解 - NTT docomo Business Engineers' Blog](https://engineers.ntt.com/entry/20251208_advent-calendar-day8/entry)
- **公開日:** 2025-12-08

## いつ読むか？

- テストダブルに関する用語の整理をしたいとき
- テストダブルに関する用語の使い分けについて教えたいとき

## 読書メモ

xUTP（xUnit Test Patterns）によるテストダブルの分類。

テストダブルは関心領域で3つに整理できる。

**間接出力への関心**（SUT が依存コンポーネントに送るデータ）
- Mock: 検証する（事前に期待値を設定し、呼ばれたか確認）
- Spy: 記録する（実行後に呼び出し内容を検証）

**間接入力への関心**（依存コンポーネントから受け取るデータ）
- Stub: 操作する（現在時刻の固定など、テストに都合のいい値を返す）

**実装への関心**
- Fake: 置換する（本物より高速なインメモリ実装やエミュレーターで代替）

**Dummy** は xUTP では厳密にはテストダブルでなく「値パターン」に分類される。
