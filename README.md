# 🧠 Agent Skills Collections

AIエージェント向けの再利用可能なSkills（スキル）集です。

## 対象エージェント

| エージェント       | 説明                                                   |
| ------------------ | ------------------------------------------------------ |
| **Antigravity**    | Google DeepMind のエージェントコーディングアシスタント |
| **RooCode**        | VS Code 拡張のAIコーディングエージェント               |
| **GitHub Copilot** | GitHub のAIペアプログラマー                            |

## Skill 一覧


<!-- 以下のフォーマットでSkillを追加してください：
| [skill-name](./collections/skill-name/) | 説明 | `tag1`, `tag2` |
-->

| Skill                                                           | 説明                                      | タグ                          |
| --------------------------------------------------------------- | ----------------------------------------- | ----------------------------- |
| [connect_ssh](./collections/connect_ssh/)                       | .envの接続情報を使用してSSH接続を確立する | `ssh`, `remote`, `connection` |
| [python-static-analysis](./collections/python-static-analysis/) | flake8でPythonコードを静的解析し修正する  | `python`, `lint`, `flake8`    |

## ディレクトリ構成

各Skillは以下の構成で管理されています：

```
skill-name/
├── SKILL.md              # 必須：メタデータと主要指示
├── scripts/              # オプション：実行可能コード
├── references/           # オプション：追加ドキュメント
└── assets/               # オプション：テンプレート、リソース
```

### SKILL.md

各Skillの中核となるファイルです。YAMLフロントマターでメタデータを定義し、Markdownで詳細な指示・手順を記述します。

```yaml
---
name: skill-name
description: スキルの簡潔な説明
version: "1.0.0"
target_agents:
  - antigravity
  - roocode
  - github-copilot
languages:
  - python
  - shell
tags:
  - カテゴリタグ
---
```

## 使い方

このリポジトリから使いたいSkillを選び、各エージェントの所定の場所にコピーして使用します。

### Antigravity

Skillフォルダをワークスペースルートまたは `.agent/skills/` 配下にコピーします。
`SKILL.md` がエージェントのコンテキストとして自動で認識されます。

```
your-project/
├── .agent/
│   └── skills/
│       └── skill-name/       ← collections/ からコピー
│           └── SKILL.md
└── src/
```

### RooCode

Skillフォルダを `.roo/skills/`（プロジェクト単位）または `~/.roo/skills/`（グローバル）にコピーします。
RooCode v3.38.0 以降で、リクエストに応じてSkillが自動で読み込まれます。

```
your-project/
├── .roo/
│   └── skills/
│       └── skill-name/       ← collections/ からコピー
│           └── SKILL.md
└── src/
```

グローバルに使いたい場合：

```
~/.roo/
└── skills/
    └── skill-name/           ← collections/ からコピー
        └── SKILL.md
```

### GitHub Copilot

Skillの内容を `.github/copilot-instructions.md`（リポジトリ全体）に記述するか、
`.github/instructions/` 配下にパス指定付きのインストラクションファイルとして配置します。

```
your-project/
├── .github/
│   ├── copilot-instructions.md    ← Skillの内容を転記（リポジトリ全体に適用）
│   └── instructions/
│       └── skill-name.instructions.md  ← パス指定で特定ファイルに適用
└── src/
```

> **Note**: GitHub Copilot は `SKILL.md` 形式を直接認識しないため、内容を上記ファイルに転記してください。

## 主な技術スタック

- **Python** 3.10+
- **Bash** / シェルスクリプト
- その他、Skillに応じて追加

## ライセンス

MIT License

## 貢献方法

1. `collections/` ディレクトリ内に、Skill名（kebab-case）のフォルダを作成する
2. `SKILL.md` を作成し、YAMLフロントマターとスキルの説明・手順を記述する
3. 必要に応じて `scripts/`, `references/`, `assets/` を追加する
4. このREADMEのSkill一覧テーブルを更新する

```
collections/
└── your-new-skill/
    ├── SKILL.md              # 必須
    ├── scripts/              # オプション
    ├── references/           # オプション
    └── assets/               # オプション
```
