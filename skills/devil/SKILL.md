---
name: devil
description: "変更に対して品質+セキュリティの批判的レビュー。懸念ゼロまで収束させる"
argument-hint: "[path] [--fix]"
triggers:
  - review
  - レビュー
  - 品質
  - セキュリティ
  - 懸念
  - チェック
---

# /devil — Devil's Advocate Review

変更差分に対して品質 + セキュリティの批判的レビュー。懸念ゼロまで収束させる。

- **引数なし** → git diff の全変更をレビュー
- **パス指定** → そのパス以下の変更のみ
- **--fix** → レビュー → Critical/Warning を自動修正 → 再レビュー

## 手順

### 1. 変更範囲の特定

```bash
git diff --stat
git diff --cached --stat
git log --oneline -5
```

### 2. 批判的レビュー

**品質観点**:
- ロジックバグ・エッジケース・off-by-one
- パフォーマンス問題（N+1, 不要なループ, メモリリーク）
- 既存パターンとの不整合
- エラーハンドリングの欠如

**セキュリティ観点（OWASP Top 10）**:
- インジェクション（SQL / コマンド / パストラバーサル）
- 認証・認可の欠如
- 機密情報の露出（トークン・パスワード・APIキー）
- 入力バリデーション不足
- XSS / CSRF（Web UI の場合）

詳細チェックリスト → `references/devil-checklist.md`

### 3. 出力フォーマット

```markdown
## Devil's Advocate Review

### Critical Issues (must fix)
- [問題] → [対処案]

### Warnings (should fix)
- [問題] → [対処案]

### Low Risk (acceptable)
- [問題] — [放置OK の理由]

### Security Check
- [ ] Injection: パラメータバインディング / 入力サニタイズ
- [ ] Auth: エンドポイント認証・認可
- [ ] Secrets: トークン・パスワード露出なし
- [ ] XSS: ユーザー入力のエスケープ
- [ ] Validation: 外部入力のバリデーション

### Verdict
懸念数: Critical X / Warning Y / Low Risk Z
→ [対応アクション or "懸念なし — ship 可能"]
```

### 4. 収束ループ

懸念があれば修正 → 再レビュー → **懸念ゼロになるまで繰り返す**。

`--fix` の場合: レビュー → 自動修正 → 再レビューで収束確認。

$ARGUMENTS
