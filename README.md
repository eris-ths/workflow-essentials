# workflow-essentials

> Claude Code での開発を 4 つのコマンドで構造化する。

## インストール

Claude Code で以下を実行:

```
/plugin marketplace add eris-ths/workflow-essentials
/plugin install workflow-essentials@eris-ths-workflow-essentials
```

または、手動でクローンして直接読み込む:

```bash
git clone https://github.com/eris-ths/workflow-essentials.git
claude --plugin-dir ./workflow-essentials
```

インストール後、Claude Code を再起動（`/exit` → 再度起動）すれば準備完了。

### 更新

プラグインの更新後は `/reload-plugins` を実行すると、再起動なしで新バージョンが反映される。

## クイックスタート

```
/ctx          → 前回の続きから再開
/devil        → 変更をレビュー（品質 + セキュリティ）
/ship         → テスト → コミット → デプロイ
/reflect      → 学んだことを記録
```

外部サービス、データベース、事前設定は不要。

## こんな時どうする？（逆引きガイド）

### 昨日の続きから作業を再開したい

```
/ctx
```

前回 `/ctx save` で保存した文脈（何をやっていたか、次に何をするか）を自動復元。セッション終了時に `/ctx save` しておくだけ。

名前付きスロットで複数の作業文脈を管理することもできる:

```
/ctx save api          ← API作業の文脈を保存
/ctx save frontend     ← フロント作業の文脈を保存
/ctx list              ← 保存済みスロット一覧
/ctx api               ← API作業に切り替え
```

### コードを書いたけど、見落としがないか不安

```
/devil
```

品質（ロジックバグ・パフォーマンス・エッジケース）とセキュリティ（OWASP Top 10）の両面からレビュー。懸念が見つかれば修正 → 再レビューを懸念ゼロまで繰り返す。

```
/devil --fix
```

懸念の自動修正まで一気に行う。

### 実装が完了したのでリリースしたい

```
/ship
```

5 Phase を順番に実行:
1. **Review** — 品質+セキュリティレビュー（/devil）
2. **Fix** — 指摘の修正 → 再レビュー
3. **Test** — テストスイート実行
4. **Commit** — 変更をコミット
5. **Deploy** — 本番反映（設定時）

```
/ship --dry
```

デプロイせずにコミットまで。初回はこちらが安心。

### 今日やったことを次回の自分に残したい

```
/reflect
```

セッション中の学び（踏んだ罠、成功パターン、判断の理由）を .claude/ctx/learnings.md に記録。次回 `/ctx` で復元した時に活きる。

### 1日の開発フロー例

```
朝:   /ctx                    ← 昨日の続きから
      [コーディング]
昼:   /devil                  ← 午前の実装をチェック
      [修正・追加実装]
夕:   /ship                   ← まとめてリリース
      /reflect                ← 学びを記録
      /ctx save               ← 明日の自分へ引き継ぎ
```

### 1コマンドだけ使いたい

全部使う必要はない。たとえば:

- `/devil` だけ — PR前のセルフレビューとして
- `/ctx` だけ — セッション間の引き継ぎメモとして
- `/ship` だけ — コミット〜デプロイの定型作業を自動化

## コマンド一覧

| コマンド | 機能 | 主なオプション |
|---------|------|---------------|
| `/ctx` | セッション文脈の保存と復元 | `save [slot]`, `load [slot]`, `list`, `delete <slot>` |
| `/devil` | 懸念収束型の批判的レビュー | `--fix`（自動修正） |
| `/ship` | 5 Phase の出荷フロー | `--dry`, `--skip-test` |
| `/reflect` | 学びを .claude/ctx/learnings.md に記録 | `--clean`（整理） |

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

22 以上のプロジェクトを通じて磨かれた開発ワークフローから、汎用部分を抽出・簡素化したもの。

---

*v1.1.1 — 2026-03-14*
