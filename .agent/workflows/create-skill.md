---
description: 新しいSkillを作成する手順
---

# 新しいSkillの作成

## 手順

1. リポジトリルートに `skill-name/` ディレクトリを作成する（kebab-case）
2. `SKILL.md` を作成し、YAMLフロントマターとスキルの説明・手順を記述する
3. 必要に応じて以下のサブディレクトリを追加する：
   - `scripts/` — 実行可能コード（Python, Shell）
   - `references/` — 追加ドキュメント
   - `assets/` — テンプレート、リソース
4. ルートの `README.md` のSkill一覧テーブルを更新する

## SKILL.md テンプレート

```yaml
---
name: skill-name
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
  - category
---
```

```markdown
# Skill Name

## 概要
このスキルの目的と何を解決するかを説明する。

## 使い方
1. 手順1
2. 手順2

## 入出力例
### 入力
（サンプル入力）

### 出力
（期待される出力）
```
