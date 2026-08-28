---
title: "xUTPによるテストダブルの定義とその図解 - NTT docomo Business Engineers' Blog"
created: 2026-03-26
modified: 2026-03-26
permalink: bbf791c403d4
tags:
  - TDD
  - テストダブル
URL: https://engineers.ntt.com/entry/20251208_advent-calendar-day8/entry
著者:
公開日: 2025-12-08
開始日: 2026-03-26
終了日: 2026-03-26
---
# 読書メモ: xUTPによるテストダブルの定義とその図解 - NTT docomo Business Engineers' Blog

- **URL:** [xUTPによるテストダブルの定義とその図解 - NTT docomo Business Engineers' Blog](https://engineers.ntt.com/entry/20251208_advent-calendar-day8/entry)
- **公開日:** 2025-12-08

## いつ読むか？

- テストダブルの種類（モック・スタブなど）を使い分けたいとき。

## 読書メモ

xUnit Test Patterns (xUTP) に基づくテストダブルの分類。

**登場人物**

- SUT（テスト対象）
- DOC（SUTが依存するコンポーネント）
- 直接入出力: テスト ↔ SUT 間
- 間接入出力: SUT ↔ DOC 間

**テストダブル4分類**

| 種類   | 目的              | 例                |
| ---- | --------------- | ---------------- |
| スタブ  | 間接入力を操作（固定値を返す） | 時刻関数を固定値に差し替え    |
| スパイ  | 間接出力を記録（後で検証）   | 呼び出し引数を記録        |
| モック  | 間接出力を検証（呼び出し確認） | SQL文・APIリクエストの検証 |
| フェイク | 実装ごと置換（軽量な代替実装） | DBをメモリ実装に差し替え    |

※ダミーはテストダブルではないとして除外されている。

**ポイント**: モックは「検証」、スパイは「記録」、スタブは「入力操作」、フェイクは「実装置換」という関心の違いで区別する。
