---
name: connect-ssh
description: .envファイルの接続情報を使用してSSH接続を確立する
version: "1.0.0"
target_agents:
  - antigravity
  - roocode
  - github-copilot
languages:
  - shell
tags:
  - ssh
  - remote
  - connection
---

# Connect SSH

プロジェクトルートの `.env` ファイルからSSH接続情報を読み取り、リモートマシンへのSSH接続を確立するスキル。

## トリガー

### Antigravity

ワークスペース内にこの `SKILL.md` があれば自動で認識される。
ユーザーのリクエストがこのスキルの内容に関連すると判断した場合、エージェントが `SKILL.md` を読み込んで手順を実行する。

**トリガーとなるプロンプト例：**
- `SSHで接続して`
- `リモートサーバーに接続したい`
- `.envの設定を使ってSSH接続して`
- `サーバーにログインして`

### RooCode

`.roo/skills/connect_ssh/` にこのSkillフォルダを配置すると自動で認識される。
フロントマターの `description` をもとに、ユーザーのリクエストにマッチした場合にスキルが自動ロードされる。

**トリガーとなるプロンプト例：**
- `SSHで接続して`
- `リモートマシンに繋ぎたい`
- `connect-ssh スキルを使って接続して`（スキル名で直接指定も可）

### GitHub Copilot

Copilot は `SKILL.md` を直接認識しないため、内容を `.github/copilot-instructions.md` または `.github/instructions/connect-ssh.instructions.md` に転記する必要がある。
転記後は、該当するリクエストに対してCopilotが指示に従って動作する。

**トリガーとなるプロンプト例：**
- `SSH接続して`
- `.envを読み取ってサーバーに接続して`

## 前提条件

- ローカルマシンに `ssh` がインストールされていること
- プロジェクトルートに `.env` ファイルが作成済みであること
- リモートマシンのSSHサーバーが起動していること

### Windows環境の場合

Windowsでは `ssh` コマンドを使用するために **WSL（Windows Subsystem for Linux）** の起動が必要な場合がある。

```bash
# WSLを起動
wsl

# WSL内でsshが利用可能か確認
which ssh
```

> **注意**: Windows標準のコマンドプロンプトやPowerShellにも `ssh` が搭載されているが、
> `.env` の読み込み（`export` コマンド）はbash/zshを前提としているため、WSLの使用を推奨する。

## .env ファイルの書式

プロジェクトルートに `.env` ファイルを作成し、以下の変数を定義する。
テンプレートとして `.env.example` を参照のこと。

```env
SSH_HOST=192.168.1.100    # 必須：リモートマシンのIPアドレスまたはホスト名
SSH_USER=ubuntu           # 必須：SSHログインユーザー名
SSH_PORT=22               # 任意：SSHポート番号（デフォルト: 22）
```

> **注意**: `.env` ファイルには機密情報が含まれるため、必ず `.gitignore` に追加すること。

## SSH接続手順

### 1. .env ファイルの存在確認

```bash
# プロジェクトルートに .env があるか確認
if [ ! -f .env ]; then
  echo "❌ .env ファイルが見つかりません。.env.example を参考に作成してください。"
  exit 1
fi
```

### 2. .env の読み込み

```bash
# .env から変数を読み込む
export $(grep -v '^#' .env | xargs)
```

### 3. SSH接続の実行

```bash
# SSH接続（ポート指定あり）
ssh -p "${SSH_PORT:-22}" "${SSH_USER}@${SSH_HOST}"
```

このコマンドを実行すると、パスワード入力のプロンプトが表示される。
**パスワードの入力はユーザーが手動で行う。**

### 一連のコマンド（コピー用）

```bash
export $(grep -v '^#' .env | xargs) && ssh -p "${SSH_PORT:-22}" "${SSH_USER}@${SSH_HOST}"
```

## 接続確認

接続テストのみ行いたい場合（ログインせずに確認）：

```bash
export $(grep -v '^#' .env | xargs) && ssh -p "${SSH_PORT:-22}" -o ConnectTimeout=5 "${SSH_USER}@${SSH_HOST}" "echo 'Connection OK'"
```

## トラブルシューティング

### 接続できない場合

```bash
# 詳細ログで接続を試行
export $(grep -v '^#' .env | xargs) && ssh -vvv -p "${SSH_PORT:-22}" "${SSH_USER}@${SSH_HOST}"
```

### よくある原因

| 症状                 | 原因                                | 対処                                                          |
| -------------------- | ----------------------------------- | ------------------------------------------------------------- |
| Connection refused   | SSHサーバーが停止 / ポートが違う    | リモート側で `sudo systemctl status sshd` を確認              |
| Connection timed out | ファイアウォール / IPアドレスが違う | `.env` の `SSH_HOST` を確認、ネットワーク疎通を `ping` で確認 |
| Permission denied    | ユーザー名またはパスワードが違う    | `.env` の `SSH_USER` を確認                                   |
| No route to host     | ネットワーク到達不可                | VPN接続やネットワーク設定を確認                               |
