---
description: "5 Phase の出荷フロー。レビュー → 修正 → テスト → コミット → デプロイ"
tags: [workflow, deploy, ship]
---

# /ship — Ship It

品質を保証してから出荷する。5つの Phase を順に実行。

**使い方**: `/ship [--dry] [--skip-test]`

## 引数

- **引数なし** → 全 Phase 実行
- **--dry** → Phase 1-2 のみ（レビュー + 修正まで）
- **--skip-test** → Phase 3 をスキップ（テストがないプロジェクト向け）

## 5 Phases

### Phase 1: Review（/devil）

変更差分に対して品質 + セキュリティレビューを実行。
`/devil` コマンドと同等。

### Phase 2: Fix

Phase 1 の指摘を修正。
- Critical / Warning があれば修正して再レビュー
- 指摘なしならスキップ

### Phase 3: Test

プロジェクトのテストコマンドを実行。

```yaml
設定ファイル: ".claude/ship.yml"
デフォルト: "テストコマンドが未設定ならスキップ"
失敗時: "required: true なら停止、false なら警告して続行"
```

### Phase 4: Commit

変更をコミット。
- コミットメッセージを変更内容から自動生成
- conventional commits 形式（設定可能）

### Phase 5: Deploy

デプロイコマンドを実行（設定されている場合のみ）。
- `confirm: true` なら実行前に確認を求める
- 未設定ならスキップ

## 設定ファイル

`.claude/ship.yml`（プロジェクトルートに配置）:

```yaml
# テストコマンド（Phase 3）
test:
  command: "npm test"          # or "pytest", "go test ./...", etc.
  required: true               # false ならテスト失敗でも続行

# デプロイコマンド（Phase 5, 任意）
deploy:
  command: "gcloud run deploy"
  confirm: true                # 実行前に確認

# コミット設定（Phase 4）
commit:
  convention: "conventional"   # "conventional" | "freeform"
```

設定ファイルがない場合:
- Phase 3: スキップ
- Phase 4: conventional commits 形式
- Phase 5: スキップ

## 設計原則

```yaml
自己完結: "外部ツール・サービスへの依存なし"
設定で拡張: "ship.yml でプロジェクトごとにカスタマイズ"
段階的: "--dry で安全に試せる"
```

$ARGUMENTS
