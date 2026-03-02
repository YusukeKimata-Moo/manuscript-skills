# Skills for Academic Manuscript Writing

分子生物学の学術論文原稿を執筆・校正・英訳するための AI コーディングエージェント用スキルセットです。Claude Code、Codex、Antigravity など、`.agent/skills/` や `~/.agents/skills/` を認識するエージェントで共通して使用できます。

### スキル一覧

| スキル                     | 説明                                                                                           |
| -------------------------- | ---------------------------------------------------------------------------------------------- |
| **manuscript-review**      | 原稿の論理構造・セクション間整合性・用語の一貫性をチェックし、修正を支援（日本語・英語両対応） |
| **manuscript-translation** | 日本語原稿を英訳しやすい文体に校正 → 学術英語に翻訳 → 英文校閲。英文校正のみの単独利用も可     |

> 両スキルが共通で参照する日本語修正パターン集は `shared-references/` に格納されています。

### セットアップ

プロジェクトの `.agent/skills/` ディレクトリにスキルフォルダをコピーしてください。

```
your-project/
└── .agent/
    └── skills/
        ├── shared-references/          # 両スキル共通のリファレンス
        │   ├── japanese_patterns.md
        │   └── journal_guidelines.md   # ジャーナル投稿規定テンプレート（要記入）
        ├── manuscript-review/
        │   ├── SKILL.md
        │   └── references/             # チェックリスト・レポート形式
        └── manuscript-translation/
            ├── SKILL.md
            └── references/             # 時制ルール・表現ガイド
```

```bash
# リポジトリをクローンし、スキルをコピー
git clone https://github.com/YusukeKimata-Moo/manuscript-skills.git
cp -r manuscript-skills/shared-references .agent/skills/
cp -r manuscript-skills/manuscript-review .agent/skills/
cp -r manuscript-skills/manuscript-translation .agent/skills/
```

スキルは対応するエージェント（Claude Code、Codex、Antigravity 等）が自動的に検出します。追加の設定は不要です。

### 使い方

使用前に `shared-references/journal_guidelines.md` に投稿先ジャーナルの規定を記入してください。スキルがレビュー・翻訳時にこの情報を参照します。

エージェントに論文原稿の精査や英訳を依頼すると、関連するスキルが自動的に参照されます。

**例：原稿レビュー**

```
Introduction, Results, Discussion の内容を精査し、セクション間の整合性を確認せよ
```

**例：英訳**

```
Discussion セクションを学術英語に翻訳せよ
```

**例：英文校正**

```
Discussion セクションの英文を校正せよ
```

### 想定する使用環境

- 日本語で原稿を執筆し、最終的に英訳するワークフロー
- セクションごとに個別のMarkdownファイルで管理する原稿構成
- 分子生物学・生命科学分野の学術論文（他分野にも応用可能）
- 典型的な連携フロー: `manuscript-review`（構造・一貫性チェック＋日本語校正） → `manuscript-translation`（英訳＋英文校閲）

