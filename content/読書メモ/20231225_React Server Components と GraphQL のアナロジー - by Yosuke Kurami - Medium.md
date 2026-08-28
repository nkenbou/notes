---
permalink: 73c2367f7c49
tags:
  - React
  - RSC
  - NextJS
URL: https://quramy.medium.com/react-server-components-%E3%81%A8-graphql-%E3%81%AE%E3%82%A2%E3%83%8A%E3%83%AD%E3%82%B8%E3%83%BC-89b3f5f41a01
著者: "@Quramy"
公開日: 2023-12-25
開始日:
終了日:
---
# 読書メモ: React Server Components と GraphQL のアナロジー | by Yosuke Kurami | Medium

- **URL:** [React Server Components と GraphQL のアナロジー | by Yosuke Kurami | Medium](https://quramy.medium.com/react-server-components-%E3%81%A8-graphql-%E3%81%AE%E3%82%A2%E3%83%8A%E3%83%AD%E3%82%B8%E3%83%BC-89b3f5f41a01)
- **著者:** @Quramy
- **公開日:** 2023-12-25

## いつ読むか？

- React Server Component の理解を深めたいとき

## 読書メモ

### 核心

RSC と GraphQL (Relay) は「コンポーネントが自身の必要なデータを要求する」という同じ設計思想を持つ。

### 要点

- **自律分散データ取得**: データ取得を中央集権ではなく、各コンポーネントに分散させる
- **ストリーミング**: Async Component を Suspense で囲むことで、準備できた部分から順次表示
- **GraphQL の @defer**: 同様のことが可能だが、2023年12月時点でまだ RFC 段階。RSC に先を越された形

### 実践への適用

- コンポーネント設計時に「このコンポーネントが必要とするデータは何か」を考える
- データ取得ロジックをページ全体で一括管理するのではなく、各コンポーネントに持たせる
- Suspense を活用して段階的なコンテンツ表示を実現する
