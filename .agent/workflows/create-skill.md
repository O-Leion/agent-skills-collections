---
description: 新しいSkillを作成する手順
---

# 新しいSkillの作成

## 手順

1. `collections/` 内に `skill-name/` ディレクトリを作成する（kebab-case）
2. `SKILL.md` を作成し、YAMLフロントマターとスキルの説明・手順を記述する
3. `README.md` を作成し、GitHub上でスキルの概要が分かるようにする
4. 必要に応じて以下のサブディレクトリを追加する：
   - `scripts/` — 実行可能コード（Python, Shell）
   - `references/` — 追加ドキュメント
   - `assets/` — テンプレート、リソース
5. **ルートの `README.md` のSkill一覧テーブルにリンク付きで追記する**

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

## README.md テンプレート

Skillごとの `README.md` はGitHub上での説明用です。以下を参考に作成してください：

```markdown
# Skill Name

## 概要
このスキルが何をするか、どのような場面で使うかを説明する。

## 対象エージェント
- Antigravity / RooCode / GitHub Copilot

## 主な機能
- 機能1
- 機能2

## 使い方
各エージェントへの導入方法はルートの [README.md](../../README.md#使い方) を参照。

## ファイル構成
| ファイル         | 説明                             |
| ---------------- | -------------------------------- |
| `SKILL.md`       | エージェント向けメタデータと指示 |
| `scripts/xxx.py` | 〇〇用スクリプト                 |
```
