# Skill ディレクトリ構成ルール

各Skillは以下の構成に従ってください：

```
skill-name/
├── SKILL.md              # 必須：メタデータと主要指示
├── scripts/              # オプション：実行可能コード
│   ├── analyze.py
│   └── validate.sh
├── references/           # オプション：追加ドキュメント
│   ├── api-reference.md
│   └── examples.md
└── assets/               # オプション：テンプレート、リソース
    └── template.json
```

## SKILL.md のフォーマット

すべてのSKILL.mdファイルは以下のYAMLフロントマターで始めてください：

```yaml
---
name: スキル名（英語、kebab-case）
description: スキルの簡潔な説明（1行）
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

フロントマターの後に、Markdownで詳細な指示・手順を記述します。

## 品質基準

- 各Skillは単体で動作可能であること（他Skillへの依存を最小限にする）
- SKILL.mdだけ読めばスキルの目的と使い方が理解できること
- スクリプトにはエラーハンドリングを含めること
- サンプル入出力があると望ましい
