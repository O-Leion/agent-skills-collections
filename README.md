# 🧠 Agent Skills Collections

AIエージェント向けの再利用可能なSkills（スキル）集です。

## 対象エージェント

| エージェント       | 説明                                                   |
| ------------------ | ------------------------------------------------------ |
| **Antigravity**    | Google DeepMind のエージェントコーディングアシスタント |
| **RooCode**        | VS Code 拡張のAIコーディングエージェント               |
| **GitHub Copilot** | GitHub のAIペアプログラマー                            |

## Skill 一覧

> 現在、Skillはまだ登録されていません。今後追加予定です。

<!-- 以下のフォーマットでSkillを追加してください：
| [skill-name](./skill-name/) | 説明 | `tag1`, `tag2` |
-->

| Skill         | 説明 | タグ |
| ------------- | ---- | ---- |
| *coming soon* | —    | —    |

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

### Antigravity

Antigravityでは、Skillsフォルダがワークスペース内にあれば自動的に認識されます。`SKILL.md` の内容がエージェントのコンテキストとして利用されます。

### RooCode

RooCodeでは、カスタムモードやワークフローとしてSkillを読み込むことができます。`SKILL.md` を参照してエージェントに指示を与えます。

### GitHub Copilot

GitHub Copilotでは、Skillの内容をプロンプトやカスタムインストラクションに組み込んで使用できます。

## 主な技術スタック

- **Python** 3.10+
- **Bash** / シェルスクリプト
- その他、Skillに応じて追加

## ライセンス

MIT License

## 貢献方法

1. 新しいSkillディレクトリを作成
2. `SKILL.md` にメタデータと手順を記述
3. 必要に応じてスクリプト・リファレンス・アセットを追加
4. このREADMEのSkill一覧を更新
