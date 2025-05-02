# Hello FastAPI Docker Sample

このリポジトリは FastAPI アプリを Docker 化し、GitHub Actions で自動テスト・ビルド・
GHCR への push、および VPS への自動デプロイまでを行う最小構成サンプルです。

## 構成
- **main.py**: FastAPI “Hello, World” エンドポイント
- **tests/**: pytest による単体テスト
- **Dockerfile**: slim ベースでアプリをコンテナ化
- **.devcontainer/**: VS Code Dev Container 設定
- **.github/workflows/**:
  - `ci.yml`  : push ごとに `pytest` 実行
  - `docker.yml` : バージョンタグ push で GHCR へビルド & push
  - `deploy.yml`: GHCR イメージ更新に連動して VPS へ自動デプロイ
- **docker-compose.example.yml**: VPS 側で使用する compose ファイル例

## 使い方
1. GitHub に空のリポジトリを作成し、本ファイル群を push。
2. リポジトリ `Settings → Secrets and variables → Actions` で
   `CR_PAT`, `SSH_HOST`, `SSH_USER`, `SSH_KEY` を登録。
3. デプロイ先 VPS に `docker-compose.example.yml` を `/srv/app/docker-compose.yml`
   として配置。
4. ローカルで `git tag v0.1.0 && git push --tags`。
   → `Docker Build & Push` → `Deploy` ワークフローが自動実行されます。
