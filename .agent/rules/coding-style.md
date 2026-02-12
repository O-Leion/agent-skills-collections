# コーディング規約

## Python
- Python 3.10+ を対象とする
- 型ヒント（type hints）を積極的に使用する
- docstringはGoogle Styleで記述する
- フォーマッターは `ruff format`、リンターは `ruff check` を推奨する

## シェルスクリプト
- `#!/usr/bin/env bash` をshebangに使用する
- `set -euo pipefail` を先頭に記述する
- ShellCheckで検証可能な記述を心がける

## 共通
- ファイル末尾に改行を入れる
- インデントはスペース（Pythonは4、YAML/JSONは2）
- コメントやドキュメントは日本語・英語どちらでも可（一貫性を保つ）

## 命名規則

| 対象              | 規則       | 例                                 |
| ----------------- | ---------- | ---------------------------------- |
| Skillディレクトリ | kebab-case | `code-review`, `api-doc-generator` |
| Pythonファイル    | snake_case | `analyze_code.py`                  |
| シェルスクリプト  | kebab-case | `run-validation.sh`                |
| アセットファイル  | kebab-case | `config-template.json`             |
