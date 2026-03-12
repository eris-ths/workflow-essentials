---
description: "セッション文脈の保存と復元。次回の自分へのメモ"
tags: [context, session, workflow]
---

# /ctx — Session Context

セッションの状態を保存し、次回復元する。
覚えることは2つだけ: save と load。

**使い方**: `/ctx [save|load]`

## 引数

- **引数なし** → load（最も頻繁な操作を最短に）
- **save** → 現在のセッション状態を保存
- **load** → 前回の状態を復元

## 手順

### /ctx save

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

### /ctx load（または /ctx）

1. `.claude/ctx/resume.md` を読む
2. 前回の状態サマリーを表示
3. 推奨される次のアクションを提示

## 設計原則

```yaml
2操作だけ: "save と load。覚えることがほぼない"
1ファイル: ".claude/ctx/resume.md にすべて"
自分へのメモ: "次の自分（次セッションの AI）への引き継ぎ書"
```

$ARGUMENTS
