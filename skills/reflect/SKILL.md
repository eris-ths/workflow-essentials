---
name: reflect
description: "セッションの学びを .claude/ctx/learnings.md に構造化して記録する"
argument-hint: "[--clean]"
triggers:
  - reflect
  - 振り返り
  - 学び
  - 記録
---

# /reflect — Learning Record

セッションの学びを振り返り、`.claude/ctx/learnings.md` に記録する。
MEMORY.md はユーザーが管理するファイルのため、上書きを避けて専用ファイルに分離する。

- **引数なし** → セッションの学びを記録
- **--clean** → learnings.md の古い・重複した記録を整理

## /reflect

1. セッションの振り返り:
   - 変更した内容を確認
   - エラーや問題の解決過程を振り返る
   - 重要な判断とその理由を整理

2. 記録すべき学びを抽出:
   - 新しいパターン（次も使える手順やコマンド）
   - 踏んだ罠（原因 + 回避策）
   - 重要な判断（選択肢 + 理由 + 結果）

3. `.claude/ctx/learnings.md` に構造化して追記:

```markdown
## YYYY-MM-DD: [タスク名]
- **What**: 何をしたか
- **Learned**: 何を学んだか
- **Trap**: 踏んだ罠（あれば）
- **Decision**: 重要な判断（あれば）
```

## /reflect --clean

1. `.claude/ctx/learnings.md` を読む
2. 古い記録、重複した記録、もう不要な記録を特定
3. 整理案を提示 → 承認後に実行

## 記録しないもの

- 単純なファイル編集・軽微な修正
- 一般的な知識（AI が元々知っていること）
- 一回きりの作業で再現性がないもの

## 設計原則

```yaml
既存ファイルを壊さない: ".claude/ctx/learnings.md に分離。ユーザーの MEMORY.md には触れない"
200行目安: "超えたら --clean で棚卸し"
実用本位: "次の自分が助かる情報だけ残す"
```

$ARGUMENTS
