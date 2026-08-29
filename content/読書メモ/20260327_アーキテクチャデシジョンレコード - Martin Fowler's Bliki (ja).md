---
title: "読書メモ: アーキテクチャデシジョンレコード - Martin Fowler's Bliki (ja)"
created: 2026-03-27
modified: 2026-03-27
tags:
  - ADR
URL: https://bliki-ja.github.io/ArchitectureDecisionRecord
著者: Martin Fowler (@martinfowler)
公開日: 2026-03-24
開始日: 2026-03-24
終了日: 2026-03-24
---
- **URL:** [アーキテクチャデシジョンレコード - Martin Fowler's Bliki (ja)](https://bliki-ja.github.io/ArchitectureDecisionRecord)
- **著者:** Martin Fowler (@martinfowler)
- **公開日:** 2026-03-24

## いつ読むか？

- アーキテクチャの意思決定をチームで記録・共有したいとき

## 読書メモ

ADR（Architecture Decision Record）は、システムの重要な設計決定を記録する短い文書（通常1ページ以内）。

**何を書くか**
- 決定の内容と背景
- 検討した代替案とその長所・短所
- 決定の影響と信頼度

**運用ルール**
- ソースコードと同じリポジトリの `doc/adr/` に連番で保存（例: `0001-use-htmx.md`）
- ステータスは proposed / accepted / superseded で管理
- 決定を変えるときは既存を修正せず、新規ADRを作成して置き換え履歴を残す

**効果**
- 数年後でも「なぜこの設計か」を理解できる
- 書くプロセス自体でチーム内の意見相違が表面化し、議論できる
