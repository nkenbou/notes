---
permalink: ae915ac6c52c
tags:
  - Docker
  - DockerCompose
URL: https://future-architect.github.io/articles/20240620a/
著者: 市川燿
公開日: 2024-06-20
開始日:
終了日:
---
# 読書メモ: 個人的docker composeおすすめtips 9選 | フューチャー技術ブログ

- **URL:** [個人的docker composeおすすめtips 9選 | フューチャー技術ブログ](https://future-architect.github.io/articles/20240620a/)
- **著者:** 市川燿
- **公開日:** 2024-06-20

## いつ読むか？

- Docker のベストプラクティスをキャッチアップしたいとき (2024年6月20日時点)

## 読書メモ

### 9つのtips

1. **docker compose cli v2** - `docker-compose` → `docker compose` を使う
2. **ファイル監視による自動更新** - `docker compose watch` でホットリロード (Sync/Rebuild/Sync+Restart)
3. **compose.yaml** - v2から推奨ファイル名が `compose.yaml` に変更
4. **プレフィックス変更** - `name:` キーでイメージ名を `${name}_${サービス名}` 形式に
5. **ヘルスチェック** - `healthcheck` でコンテナの健全性を確認
6. **依存関係** - `depends_on` で `service_started` / `service_healthy` / `service_completed_successfully` を指定
7. **--wait オプション** - 全サービスが定常状態になるまで待機
8. **profiles** - サービスをグループ化して選択的に起動
9. **version 廃止** - compose.yaml で `version:` 記述が不要に
