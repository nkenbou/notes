---
title: "Component Architecture for React Server Components"
created: 2026-08-06
modified: 2026-08-06
permalink: 59cf676dc1cd
tags:
  - React
  - ReactServerComponents
  - アーキテクチャ
URL: https://aurorascharff.no/posts/component-architecture-for-react-server-components/
著者: Aurora Scharff
公開日: 2026-05-22
開始日: 2026-08-06
終了日: 2026-08-06
---
# 読書メモ: Component Architecture for React Server Components

- **URL:** [Component Architecture for React Server Components](https://aurorascharff.no/posts/component-architecture-for-react-server-components/)
- **著者:** Aurora Scharff
- **公開日:** 2026-05-22

## いつ読むか？

- RSC を使ったアプリの構成を新規に設計するとき、全体のベストプラクティスを確認したいとき
- 個別にキャッチアップした RSC 関連の技術要素 (Suspense、`cache()`、`'use client'`) が何を解決するのか、位置づけを整理したいとき
- page にデータ取得が集中して、コンポーネントが再利用しづらくなってきたと感じたとき
- コンポーネントのディレクトリ構成 (features 分割、Atomic Design との対応) を決めるとき
- Suspense や skeleton の置き場所をチームで議論するとき

## 読書メモ

RSC の設計原則を**全体像として**整理できる記事。

- **page は composer** (同期・データを取得しない)、**各コンポーネントが自分でデータを取得**する。loader パターンの密結合を解消し、再利用性が上がる
- `cache()` でレンダーツリー横断の**リクエスト重複排除**
- **skeleton は同ファイルに co-locate** (ズレ防止)、**Suspense は page 側**に置いてローディング順序を意図的に制御
- `'use client'` は**葉ノードまで押し下げる**
- 各コンポーネントが自律的なので、**ルーティングのディレクトリから外して features 単位で管理**するのが自然 (複数ルートで再利用できる)

**サーバー性能**と**コンポーネントの自律性**の両立が RSC の本質、という視点が軸。

## 考えたこと

- **features ≒ organisms** と捉えると、Atomic Design のコンポーネント分類とディレクトリ構成の親和性が高そう (記事にはない着想)
