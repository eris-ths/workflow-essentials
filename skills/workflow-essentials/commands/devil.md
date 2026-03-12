---
description: "変更に対して批判的レビューを行い、懸念をゼロに収束させる Devil's Advocate"
tags: [quality, review, security]
---

# /devil — Devil's Advocate Review

変更差分に対して品質 + セキュリティの批判的レビューを行う。
懸念は潰すたびに減る。ゼロになったら完了。

**使い方**: `/devil [対象パス]`

## 引数

- **引数なし** → git diff の全変更をレビュー
- **パス指定** → そのパス以下の変更のみレビュー
- **--fix** → レビュー → Critical/Warning を自動修正 → 再レビュー

## 手順

### 1. 変更範囲の特定

```bash
git diff --stat            # 未ステージの変更
git diff --cached --stat   # ステージ済みの変更
git log --oneline -5       # 直近のコミット
```

パス指定がある場合:
```bash
git diff --stat -- {path}
```

git 管理外の場合は直近編集ファイルを確認。

### 2. 批判的レビュー

**品質観点**:
- ロジックバグ・エッジケース・off-by-one
- パフォーマンス問題（N+1, 不要なループ, メモリリーク）
- 既存パターンとの不整合
- エラーハンドリングの欠如
- テストカバレッジの不足

**セキュリティ観点（OWASP Top 10）**:
- インジェクション（SQL / コマンド / パストラバーサル）
- 認証・認可の欠如
- 機密情報の露出（トークン・パスワード・APIキー）
- 入力バリデーション不足
- XSS / CSRF（Web UI の場合）

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

懸念があれば修正 → 再度レビュー → **懸念ゼロになるまで繰り返す**。

`--fix` オプション付きの場合:
1. レビュー実行
2. Critical / Warning を自動修正
3. 再レビューで収束確認

収束したら「懸念なし」と明言する。

## 原則

```yaml
懸念は収束する: "潰すたびに減る。ゼロになるまで回す"
分類は明確に: "実害あり（要修正） vs 低リスク（放置OK + 理由）"
セキュリティは必須: "品質レビューだけでなく OWASP チェックも毎回"
```

$ARGUMENTS
