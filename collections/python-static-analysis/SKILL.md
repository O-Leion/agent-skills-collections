---
name: python-static-analysis
description: flake8を使用してPythonコードの静的解析を行い、指摘に基づいてコードを修正する
version: "1.0.0"
target_agents:
  - antigravity
  - roocode
  - github-copilot
languages:
  - python
  - shell
tags:
  - python
  - lint
  - flake8
  - static-analysis
  - code-quality
---

# Python Static Analysis

flake8 を使用して Python コードの静的解析を実行し、指摘内容に基づいてコードを修正するスキル。

## トリガー

### Antigravity

ワークスペース内にこの `SKILL.md` があれば自動で認識される。

**トリガーとなるプロンプト例：**
- `Pythonコードを静的解析して`
- `flake8でチェックして`
- `コードの品質をチェックして修正して`
- `リントを実行して`

### RooCode

`.roo/skills/python-static-analysis/` にこのSkillフォルダを配置すると自動で認識される。

**トリガーとなるプロンプト例：**
- `flake8を実行して`
- `Pythonコードをチェックして`
- `python-static-analysis スキルを使って`

### GitHub Copilot

内容を `.github/copilot-instructions.md` または `.github/instructions/python-static-analysis.instructions.md` に転記する必要がある。

**トリガーとなるプロンプト例：**
- `flake8でコードをチェックして修正して`
- `静的解析を実行して`

## 前提条件

- Python 3.10+ がインストールされていること
- `flake8` がインストールされていること

### flake8 のインストール確認

```bash
# flake8 がインストールされているか確認
flake8 --version
```

インストールされていない場合：

```bash
# pip でインストール
pip install flake8

# または仮想環境内で
pip install flake8
```

> **注意**: 仮想環境（venv）を使用している場合は、仮想環境をアクティベートした状態でインストール・実行すること。

## 実行手順

### Step 1: flake8 を実行して指摘を取得

#### 特定のファイルまたはディレクトリを解析する場合

```bash
# 特定のファイル
flake8 --ignore=E501 path/to/file.py

# 特定のディレクトリ
flake8 --ignore=E501 src/
```

#### プロジェクト全体を解析する場合

```bash
flake8 --ignore=E501 .
```

**オプション説明：**
- `--ignore=E501`: 行の長さ制限（79文字）の警告を無視する

### Step 2: 結果をユーザーに提示して確認を取る

flake8 の実行結果をユーザーに提示し、修正に進んでよいか確認する。

**提示フォーマット例：**

```
flake8 の解析結果（E501 除外）:

  src/main.py:10:1: F401 'os' imported but unused
  src/main.py:25:5: E302 expected 2 blank lines, got 1
  src/utils.py:3:1: W291 trailing whitespace

合計: 3件の指摘があります。修正を進めてよいですか？
```

**ユーザーの確認を得てから Step 3 に進むこと。**

### Step 3: 指摘に基づいてコードを修正

ユーザーの承認後、指摘内容に応じてコードを修正する。

#### 自動で修正できるもの（シンプルな指摘）

以下のような指摘はエージェントが判断して修正する：

| コード | 内容                           | 修正方法         |
| ------ | ------------------------------ | ---------------- |
| W291   | 末尾の空白                     | 空白を削除       |
| W292   | ファイル末尾に改行なし         | 改行を追加       |
| W293   | インデントに空白とタブが混在   | スペースに統一   |
| E301   | メソッド間の空行が不足         | 空行を追加       |
| E302   | トップレベル定義間の空行が不足 | 空行を2行に      |
| E303   | 空行が多すぎる                 | 余分な空行を削除 |
| W391   | ファイル末尾の空行             | 余分な空行を削除 |
| E711   | `== None` の比較               | `is None` に変更 |
| E712   | `== True` の比較               | `is True` に変更 |

#### ユーザーに相談すべきもの（複雑な指摘）

以下のような指摘は修正方針をユーザーに確認してから修正する：

| コード | 内容                        | 相談理由                         |
| ------ | --------------------------- | -------------------------------- |
| F401   | 未使用の import             | 意図的な import の可能性がある   |
| F841   | 未使用の変数                | 今後使用する予定かもしれない     |
| E741   | 曖昧な変数名（`l`, `O` 等） | 命名規則の判断が必要             |
| C901   | 関数の複雑度が高い          | リファクタリング方針の相談が必要 |

### Step 4: 修正後の再チェック

修正が完了したら、再度 flake8 を実行して指摘が解消されたことを確認する。

```bash
flake8 --ignore=E501 <対象パス>
```

指摘が0件になるまで Step 3〜4 を繰り返す。

## flake8 主要エラーコード一覧（参考）

| プレフィックス | カテゴリ   | 例                                    |
| -------------- | ---------- | ------------------------------------- |
| E1xx           | インデント | E111: インデントが4の倍数でない       |
| E2xx           | 空白       | E231: `:` の後に空白がない            |
| E3xx           | 空行       | E302: トップレベル定義間の空行不足    |
| E4xx           | import     | E401: 1行に複数の import              |
| E7xx           | 文の構造   | E711: `None` との比較に `==` を使用   |
| W              | 警告       | W291: 末尾の空白                      |
| F              | PyFlakes   | F401: 未使用 import, F841: 未使用変数 |
| C              | 複雑度     | C901: 関数の複雑度が高すぎる          |

## トラブルシューティング

### flake8 が見つからない場合

```bash
# Python のパスを確認
which python3
which flake8

# pip で再インストール
pip install --upgrade flake8
```

### 仮想環境での実行

```bash
# 仮想環境のアクティベート
source .venv/bin/activate  # Linux/macOS
.venv\Scripts\activate     # Windows

# flake8 実行
flake8 --ignore=E501 src/
```

### 特定のルールを追加で無視したい場合

```bash
# 複数のルールを無視
flake8 --ignore=E501,W503 src/
```
