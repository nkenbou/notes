---
permalink: 29dbcc89d579
tags:
  - React
  - jotai
URL: https://zenn.dev/uhyo/books/learn-react-with-jotai
著者: 鈴木僚太 (@uhyo)
公開日: 2026-01-03
開始日: 2026-01-09
終了日: 2026-01-24
---

# 読書メモ: jotaiによるReact再入門

- **URL:** [jotaiによるReact再入門](https://zenn.dev/uhyo/books/learn-react-with-jotai)
- **著者:** 鈴木僚太 (@uhyo)
- **公開日:** 2026-01-03

## いつ読むか？

- Suspenseやトランジションを使ったUI設計を検討するとき、この本を参照する。

## 読書メモ

### Suspense

- **Suspenseとは**: 非同期処理（データ取得など）の完了を待つ間、フォールバックUIを表示するReactの標準機構
- 従来の `isLoading` フラグによる条件分岐を不要にし、宣言的に非同期状態を扱える
- 関連章: 第3章「Suspenseの基本」、第4章「Suspenseとjotaiを組み合わせる」、第5章「AbortSignalを使って非同期処理の中断に対応する」

### トランジション

- **トランジションとは**: 状態更新の優先度を下げ、UIの応答性を保つ仕組み（`useTransition`, `startTransition`）
- `isPending` で遷移中かどうかを判定し、ローディング表示などに活用
- **世界の分岐**: トランジション中は新旧の状態が並行して存在し、新しい状態の準備が完了するまで古いUIを維持
- **オプトアウト**: `useDeferredValue` を使い、特定の値だけトランジションの影響から除外できる
- 関連章: 第7章「トランジションの基本」、第8章「トランジションと"世界の分岐"」、第9章「トランジションのオプトアウト」
