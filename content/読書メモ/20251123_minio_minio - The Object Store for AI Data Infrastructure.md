---
title: "読書メモ: minio/minio: The Object Store for AI Data Infrastructure"
created: 2025-11-23
modified: 2025-11-23
permalink: b5febaec1ca3
tags:
  - minio
  - AmazonS3
  - オブジェクトストレージ
URL: https://github.com/minio/minio
著者:
公開日:
開始日: 2025-11-23
終了日:
---
- **URL:** [minio/minio: The Object Store for AI Data Infrastructure](https://github.com/minio/minio)

## いつ読むか？

- オブジェクトストレージの選定候補として
- Amazon S3 互換のオブジェクトストレージでインフラをモックしたいとき

## 読書メモ

### MinIO とは

S3 互換のオープンソースオブジェクトストレージ（GNU AGPL v3.0）。AI/ML やデータ分析向けに高性能・スケーラブルに設計されている。

### いつ使うか

- S3 互換のローカル開発環境が必要なとき
- AI/ML ワークロード用のオブジェクトストレージを自前で構築したいとき
- プライベートクラウドに S3 互換ストレージを導入したいとき

### クイックスタート

```bash
# インストール
go install github.com/minio/minio@latest

# 起動
minio server /data
```

- Web コンソール: http://127.0.0.1:9000
- デフォルト認証: minioadmin / minioadmin

### 注意点

コミュニティ版はソースコード配布のみ（プリコンパイル済みバイナリなし）。
