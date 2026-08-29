---
title: "読書メモ: Ory HydraでOAuth2認可サーバーを構築する - じゃあ、おうちで学べる"
created: 2026-01-30
modified: 2026-01-30
tags:
  - OryHydra
  - OAuth2
  - OpenIdConnect
URL: https://syu-m-5151.hatenablog.com/entry/2026/01/04/133007
著者: "@nwiizo"
公開日: 2026-01-04
開始日: 2026-01-30
終了日: 2026-01-30
---
- **URL:** [Ory HydraでOAuth2認可サーバーを構築する - じゃあ、おうちで学べる](https://syu-m-5151.hatenablog.com/entry/2026/01/04/133007)
- **著者:** @nwiizo
- **公開日:** 2026-01-04

## いつ読むか？

- 既存の認証基盤がある状態で OAuth2/OIDC 対応が必要になったとき
- 認証方式（パスワード、パスキー、MFA 等）を自由に選びたいとき
- プロトコル層の実装を自前でやりたくないとき

## 読書メモ

Ory Hydra は「ヘッドレス」な OAuth2/OIDC 認可サーバー。認証ロジック自体は実装せず、プロトコル層に特化している。

### 核心的な特徴

- 認証をしない設計：既存のユーザー DB・認証システムをそのまま活用できる
- OAuth2/OIDC の仕様準拠部分だけを任せられる
- OpenID Connect Certification 取得済み
- PKCE、リプレイ攻撃対策などセキュリティ機構を内包

### アーキテクチャ

3 層構成：

1. **Public API（4444）** - クライアント向け OAuth2 エンドポイント
2. **Login/Consent Provider（3000）** - カスタム認証ロジックを実装する領域
3. **Admin API（4445）** - 認証結果を Hydra に通知する内部連携用
