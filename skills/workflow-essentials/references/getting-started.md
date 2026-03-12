# はじめに

## インストール

Claude Code で以下を実行:

```
/plugin marketplace add eris-ths/workflow-essentials
/plugin install workflow-essentials@eris-ths/workflow-essentials
```

または、手動でインストール:

```bash
git clone https://github.com/eris-ths/workflow-essentials.git ~/.claude/plugins/workflow-essentials
```

インストール後、Claude Code を再起動すれば準備完了。設定ファイルは不要。

## 最初のセッション

```
1. /ctx                    ← 前回のセッションがあれば復元
2. [開発作業]
3. /devil                  ← コミット前に変更をレビュー
4. /ship                   ← コミット（＋必要ならデプロイ）
5. /ctx save               ← 次回のためにセッション状態を保存
```

## ヒント

### まずは /devil から

1つだけ使うなら `/devil`。コミット前にバグとセキュリティ問題を検出する。懸念が見つかれば修正 → 再レビュー → ゼロになるまで繰り返す収束原則で、見落としを防ぐ。

### /ctx はセッション間の記憶

Claude Code のセッションは揮発性。`/ctx save` で終了時に状態を残し、`/ctx` で次回復元する。

### /ship をプロジェクトに合わせる

`.claude/ship.yml` がない場合、`/ship` は:
- `/devil` を実行（常に）
- テストをスキップ（テストコマンド未設定のため）
- conventional commit 形式でコミット
- デプロイをスキップ（デプロイコマンド未設定のため）

`ship.yml` を追加すると全パイプラインが使える。

### /reflect は任意だが蓄積する

`/reflect` の記録は未来の自分への贈り物。続けるほど、MEMORY.md がプロジェクト固有の知識ベースになり、Claude Code が毎回自動で読み込む。
