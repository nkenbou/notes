---
title: "Playwright MCPを使ってE2Eテストを楽に書く"
created: 2025-09-10
modified: 2025-09-10
permalink: 30064f4989f8
tags:
  - Playwright
  - MCP
  - E2Eテスト
  - AI
URL: https://zenn.dev/knowledgework/articles/d859f65a77fc3c
著者: "@zi"
公開日: 2025-09-10
開始日:
終了日:
---
# 読書メモ: Playwright MCPを使ってE2Eテストを楽に書く

- **URL:** [Playwright MCPを使ってE2Eテストを楽に書く](https://zenn.dev/knowledgework/articles/d859f65a77fc3c)
- **著者:** @zi
- **公開日:** 2025-09-10

## いつ読むか？

- AI で E2E テストを自動化するとき

## 読書メモ


**Playwright MCP = AIにブラウザ操作を委任できるMCP**

### 3つの活用パターン

1. **ロケーター自動生成** - Page Object Modelと組み合わせ、「ロケーターを実装して」で完了
2. **テストケース実装** - 自然言語でフローをコメント記述 → AIが実装
3. **デバッグ自動化** - HTMLレポートのTraceを使い、AIが「実行→確認→修正」を回す

### 注意点

- **トークン消費が多い** - スナップショット取得でコンテキスト圧縮が頻発
- 初回は失敗コードが出ることもある（デバッグループで修正）

### メリット

テスト内容を理解していれば、E2E未経験者やQAエンジニアも実装可能
