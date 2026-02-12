# Project Context: Agent Skills Collections

## Overview
AIエージェント（Antigravity, RooCode, GitHub Copilot）向けの再利用可能なSkills集です。
各Skillは独立したディレクトリとして管理され、`SKILL.md` を中核としたフォルダ構成に従います。

## Configuration
このプロジェクトは **Expert Configuration** を採用しています。

| 設定種別           | パス                  | 説明                                 |
| ------------------ | --------------------- | ------------------------------------ |
| グローバルルール   | `~/.gemini/GEMINI.md` | 出力言語、説明方針、全体方針         |
| プロジェクトルール | `./.agent/rules/`     | 命名規約、コーディング規約、品質基準 |
| ワークフロー       | `./.agent/workflows/` | Skill作成手順などの定型作業          |

## Tech Stack
- **Python** 3.10+（主要スクリプト言語）
- **Bash**（シェルスクリプト）
- **Markdown**（ドキュメント・SKILL定義）

## Guidelines
- **Language**: Japanese（日本語）で回答・説明
- **Code Style**: Simple & Readable
- **Skill Independence**: 各Skillは単体で動作可能であること
