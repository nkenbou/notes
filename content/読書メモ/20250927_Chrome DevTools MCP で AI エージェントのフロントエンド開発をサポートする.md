---
permalink: 296f1960ee9a
tags:
  - MCP
  - ChromeDevTools
  - AI
  - ClaudeCode
URL: https://azukiazusa.dev/blog/chrome-devtools-mcp/
著者: azukiazusa (@azukiazusa9)
公開日: 2025-09-27
開始日:
終了日:
---
# 読書メモ: Chrome DevTools MCP で AI エージェントのフロントエンド開発をサポートする

- **URL:** [Chrome DevTools MCP で AI エージェントのフロントエンド開発をサポートする](https://azukiazusa.dev/blog/chrome-devtools-mcp/)
- **著者:** azukiazusa (@azukiazusa9)
- **公開日:** 2025-09-27

## いつ読むか？

- AI で E2E テストを自動化するとき

## 読書メモ

**Chrome DevTools MCP** = AI エージェントがブラウザを自動操作できるようにするツール

**使いどき**
- フロントエンドのE2Eテスト自動化
- ブラウザのコンソールログ・ネットワークログを AI に取得させたい
- パフォーマンス分析・アクセシビリティ検査の自動化

**セットアップ（Claude Code）**
```bash
claude mcp add chrome-devtools npx chrome-devtools-mcp@latest
```

**主な機能**
- ブラウザ自動操作（Puppeteer）
- スクリーンショット撮影
- コンソール/ネットワークログ取得
- パフォーマンストレース
