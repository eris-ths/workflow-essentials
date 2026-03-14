---
name: ctx
description: "セッション文脈の保存と復元。/ctx save [slot] で保存、/ctx [slot] で復元、/ctx list で一覧"
argument-hint: "[save [slot]|load [slot]|list|delete <slot>]"
triggers:
  - context
  - session
  - 文脈
  - セッション
  - 復元
  - 引き継ぎ
---

# /ctx — Session Context

セッションの状態をスロットに保存し、次回復元する。

## Usage

| コマンド | 説明 |
|---------|------|
| `/ctx save` | デフォルトスロットに保存 |
| `/ctx save <slot>` | 名前付きスロットに保存 |
| `/ctx` or `/ctx load` | デフォルトスロットから復元 |
| `/ctx load <slot>` | 名前付きスロットから復元 |
| `/ctx list` | 保存済みスロット一覧を表示 |
| `/ctx delete <slot>` | 指定スロットを削除 |

## File Layout

```
.claude/ctx/
  resume.md              ← デフォルトスロット
  slots/
    {slot-name}.md       ← 名前付きスロット
```

## /ctx save [slot]

1. 現在のセッション状態を整理:
   - 日時、ブランチ
   - やったことの要約（2-3行）
   - 変更したファイルと内容
   - 次にやること（TODO）
   - 未解決の問題・判断待ち事項

2. 保存先を決定:
   - スロット名なし → `.claude/ctx/resume.md`
   - スロット名あり → `.claude/ctx/slots/{slot}.md`

3. ファイルに書き出す:

```markdown
# Session Context

## Last Session
- **Date**: YYYY-MM-DD HH:MM
- **Branch**: feature/xxx
- **Slot**: slot-name（名前付きの場合のみ）
- **Summary**: 何をやったか（2-3行）

## Changed Files
- path/to/file.ts — 変更内容

## Next Actions
- [ ] 次にやること

## Open Issues
- 未解決の問題・判断待ち事項
```

## /ctx load [slot]（または /ctx [slot]）

1. 保存先を決定:
   - スロット名なし → `.claude/ctx/resume.md`
   - スロット名あり → `.claude/ctx/slots/{slot}.md`
2. ファイルが存在しなければ「スロットが見つからない」旨を伝える
3. 前回の状態サマリーを表示
4. 推奨される次のアクションを提示

## /ctx list

1. `.claude/ctx/resume.md` の存在を確認（デフォルトスロット）
2. `.claude/ctx/slots/*.md` を列挙
3. 各スロットの Date と Summary 1行目を表示:

```
Saved slots:
  (default)  2026-03-14 — GCSファイラー実装
  gcs        2026-03-12 — GCS API設計
  terminal   2026-03-10 — ターミナルUI改善
```

## /ctx delete <slot>

1. `.claude/ctx/slots/{slot}.md` を削除
2. デフォルトスロットの削除は `/ctx delete default` で明示的に指定が必要（`.claude/ctx/resume.md` を削除）

$ARGUMENTS
