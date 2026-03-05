# Skills for Academic Manuscript Writing

分子生物学の学術論文原稿を執筆・校正・英訳するための AI コーディングエージェント用スキルセットです。Claude Code、Codex、Antigravity など、`.agent/skills/` や `~/.agents/skills/` を認識するエージェントで共通して使用できます。

### スキル一覧

| スキル                        | 説明                                                                                            |
| ----------------------------- | ----------------------------------------------------------------------------------------------- |
| **manuscript-review**         | 原稿の論理構造・セクション間整合性・用語の一貫性をチェックし、修正を支援（日本語・英語両対応）  |
| **manuscript-translation**    | 日本語原稿を英訳しやすい文体に校正 → 学術英語に翻訳 → 英文校閲。英文校正のみの単独利用も可      |
| **journal-guideline-checker** | ジャーナル投稿規程URLから情報を収集し、原稿のセクション構成や参考文献等のフォーマット要件を検証 |

> 各スキルが共通で参照する日本語修正パターンやジャーナル規程は `shared-references/` に格納されます。

### セットアップ

原稿のMarkdownファイルが格納されたプロジェクトの `.agent/skills/` ディレクトリにスキルフォルダをコピーしてください。

```
your-project/
└── .agent/
    └── skills/
        ├── shared-references/          # 全スキル共通のリファレンス
        │   ├── japanese_patterns.md
        │   └── journal_guidelines.md   # ジャーナル投稿規定（エージェントが自動生成）
        ├── journal-guideline-checker/
        │   └── SKILL.md
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
cp -r manuscript-skills/journal-guideline-checker .agent/skills/
cp -r manuscript-skills/manuscript-review .agent/skills/
cp -r manuscript-skills/manuscript-translation .agent/skills/
```

スキルは対応するエージェント（Claude Code、Codex、Antigravity 等）が自動的に検出します。追加の設定は不要です。

### 使い方

本ツール群は**「日本語原稿のレビュー・校正 → 英訳・英文校閲 → ジャーナル投稿規程のフォーマット確認」**という順序での使用を想定して設計されています。使い方は、エージェントへのプロンプト例を参考にしてください。

**ポイント**: 英訳・英文校正、または投稿規程チェックを依頼する前に、**投稿先ジャーナルの「Author Guidelines」等のURL**をエージェントに渡してください。エージェントが自動でサイトを巡回し、抽出したルールを `shared-references/journal_guidelines.md` に保存して複数のスキル間で共有・再利用します。

**例1：原稿レビュー（日本語）**

```
Introduction, Results, Discussion の内容を精査し、セクション間の整合性を確認せよ
```

**例2：英訳・英文校正**

```
以下の Nature の投稿規程に従って、Discussion セクションを学術英語に翻訳せよ
URL: https://www.nature.com/nature/for-authors
```

> ※すでに英訳済みの場合は「〜の英文を校正せよ」と依頼することも可能です。

**例3：ジャーナル投稿規程のフォーマット要件チェック**

```
投稿規程のルールに基づいて、原稿全体のフォーマットが規程を満たしているかチェックして
```

### 想定する使用環境

- 日本語で原稿を執筆し、最終的に英訳・投稿準備を行うワークフロー
- セクションごとに個別のMarkdownファイルで管理する原稿構成
- 分子生物学・生命科学分野の学術論文（他分野にも応用可能）
- 典型的な連携フロー: `manuscript-review`（構造・一貫性チェック） → `manuscript-translation`（指定URLからの規程保存＋英訳・英文校閲） → `journal-guideline-checker`（自動保存された規程に基づくフォーマットの最終検証）

