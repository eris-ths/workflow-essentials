---
name: ctx
description: "セッション文脈の保存と復元。/ctx save で保存、/ctx で復元"
argument-hint: "[save|load]"
triggers:
  - context
  - session
  - 文脈
  - セッション
  - 復元
  - 引き継ぎ
---

# /ctx — Session Context

セッションの状態を保存し、次回復元する。

- **引数なし** → load（前回の状態を復元）
- **save** → 現在のセッション状態を保存
- **load** → 前回の状態を復元

## /ctx save

1. 現在のセッション状態を整理:
   - 日時、ブランチ
   - やったことの要約（2-3行）
   - 変更したファイルと内容
   - 次にやること（TODO）
   - 未解決の問題・判断待ち事項

2. `.claude/ctx/resume.md` に書き出す:

```markdown
# Session Context

## Last Session
- **Date**: YYYY-MM-DD HH:MM
- **Branch**: feature/xxx
- **Summary**: 何をやったか（2-3行）

## Changed Files
- path/to/file.ts — 変更内容

## Next Actions
- [ ] 次にやること

## Open Issues
- 未解決の問題・判断待ち事項
```

## /ctx load（または /ctx）

1. `.claude/ctx/resume.md` を読む
2. 前回の状態サマリーを表示
3. 推奨される次のアクションを提示

$ARGUMENTS
