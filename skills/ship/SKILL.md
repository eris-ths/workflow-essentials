---
name: ship
description: "5 Phase の出荷フロー。レビュー → 修正 → テスト → コミット → デプロイ"
argument-hint: "[--dry] [--skip-test]"
triggers:
  - ship
  - 出荷
  - リリース
  - デプロイ
  - コミット
---

# /ship — Ship It

品質を保証してから出荷する。5つの Phase を順に実行。

- **引数なし** → 全 Phase 実行
- **--dry** → Phase 1-2 のみ（レビュー + 修正まで）
- **--skip-test** → Phase 3 をスキップ

## 5 Phases

### Phase 1: Review（/devil）

変更差分に対して品質 + セキュリティレビューを実行。

### Phase 2: Fix

Phase 1 の指摘を修正。Critical / Warning があれば修正して再レビュー。指摘なしならスキップ。

### Phase 3: Test

プロジェクトのテストコマンドを実行。

`.claude/ship.yml` の `test.command` を実行。未設定ならスキップ。
`required: true` なら失敗時停止、`false` なら警告して続行。

### Phase 4: Commit

変更をコミット。コミットメッセージを変更内容から自動生成（conventional commits 形式）。

### Phase 5: Deploy

`.claude/ship.yml` の `deploy.command` を実行。未設定ならスキップ。
`confirm: true` の場合、デプロイコマンド実行前にユーザーに確認を求める（「デプロイしますか？」と聞いて承認を待つ）。

## 設定ファイル

`.claude/ship.yml`（任意）:

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

設定ファイルがない場合: テスト=スキップ、コミット=conventional、デプロイ=スキップ。

> **注意**: `command` フィールドの値はシェルで実行されます。`ship.yml` はプロジェクトの管理者が自身で記述するファイルです。外部から取得した値や未検証の文字列を設定しないでください。

$ARGUMENTS
