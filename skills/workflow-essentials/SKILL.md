---
name: workflow-essentials
description: >-
  汎用開発ワークフロー。/ctx（文脈保存）、/devil（批判的レビュー）、
  /ship（出荷フロー）、/reflect（学習記録）の4コマンドを提供。
  Claude Code を使う全ての開発者向け。追加インフラ不要。
version: 1.0.0
user-invocable: false
triggers:
  - workflow
  - devil
  - ship
  - ctx
  - reflect
  - レビュー
  - 出荷
---

# workflow-essentials

> 開発の基本動作を4つのコマンドに凝縮。

## 4 Commands

| コマンド | 一言 | 使い方 |
|---------|------|--------|
| `/ctx` | セッション文脈の保存と復元 | `/ctx save` / `/ctx` (load) |
| `/devil` | 批判的レビュー（品質 + セキュリティ） | `/devil` / `/devil --fix` |
| `/ship` | 出荷フロー（レビュー→テスト→コミット→デプロイ） | `/ship` / `/ship --dry` |
| `/reflect` | 学びの記録 | `/reflect` / `/reflect --clean` |

## 開発フロー

```
/ctx          セッション開始。前回の続きを把握
  ↓
[開発作業]    コードを書く
  ↓
/devil        変更をレビュー。懸念をゼロに
  ↓
/ship         テスト → コミット → デプロイ
  ↓
/reflect      学びを記録。次の自分へ
  ↓
/ctx save     セッション終了。状態を保存
```

## セットアップ

1. このスキルをプロジェクトに追加
2. （任意）`.claude/ship.yml` でテスト・デプロイコマンドを設定
3. `/ctx` で開始

追加のインフラ、外部サービス、設定は不要。

## 各コマンド詳細

- `commands/ctx.md` — セッション文脈管理
- `commands/devil.md` — Devil's Advocate レビュー
- `commands/ship.md` — 出荷フロー
- `commands/reflect.md` — 学習記録

## 設計思想

```yaml
誰でも使える: "Claude Code の基本操作だけで動く。独自の概念や用語は最小限"
追加インフラ不要: "ファイルベース。DB やクラウドサービスは使わない"
段階的に使える: "/devil だけ、/ctx だけでも価値がある。全部使う必要はない"
設定より規約: "設定ファイルなしでも動く。必要に応じて ship.yml で拡張"
```

---

*v1.0.0 — 2026-03-12*
