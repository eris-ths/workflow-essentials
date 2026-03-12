# workflow-essentials

> Claude Code での開発を 4 つのコマンドで構造化する。

## クイックスタート

プラグインをインストールして、すぐに使える:

```
/ctx          → 前回の続きから再開
/devil        → 変更をレビュー（品質 + セキュリティ）
/ship         → テスト → コミット → デプロイ
/reflect      → 学んだことを記録
```

外部サービス、データベース、事前設定は不要。

## コマンド一覧

| コマンド | 機能 | 主なオプション |
|---------|------|---------------|
| `/ctx` | セッション文脈の保存と復元 | `save`, `load`（デフォルト） |
| `/devil` | 懸念収束型の批判的レビュー | `--fix`（自動修正） |
| `/ship` | 5 Phase の出荷フロー | `--dry`, `--skip-test` |
| `/reflect` | 学びを MEMORY.md に記録 | `--clean`（整理） |

## 開発フロー

```
/ctx → [開発作業] → /devil → /ship → /reflect → /ctx save
```

各コマンドは独立して動作する。1つだけでも、全部でも使える。

## オプション設定

`.claude/ship.yml` を作成すると `/ship` をカスタマイズできる:

```yaml
test:
  command: "npm test"
  required: true

deploy:
  command: "gcloud run deploy"
  confirm: true

commit:
  convention: "conventional"
```

## 設計思想

- **設定なしで動く** — インストールしたらすぐ使える
- **ファイルベース** — 外部依存なし
- **段階的に使える** — 1コマンドだけでも価値がある
- **設定より規約** — 合理的なデフォルト、必要に応じて上書き

## 出自

[Three Hearts Space](https://github.com/nao-amj/three-hearts-space) で 22 以上のプロジェクトを通じて磨かれたワークフローから、汎用部分を抽出・簡素化したもの。

---

*v1.0.0 — 2026-03-12*
