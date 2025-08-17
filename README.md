# Claude Code

## 前提条件

- [Node.js 18+](https://github.com/room202/react?tab=readme-ov-file#volta-%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)
- [Git 2.23+](https://git-scm.com/)
- [GitHub CLI](https://github.com/cli/cli)

## インストール

```bash
npm install -g @anthropic-ai/claude-code
```

## Claude Codeの起動

```bash
claude
```

## 起動失敗時の備忘録

特定のフォルダで`claude`コマンドの実行に失敗する場合、下記対象ファイルを削除すると起動した

対象ファイル : `.claude.json`と`.claude.json.backup`

対象ファイルがあるフォルダ : `C:\Users\%USERNAME%`

## VSCodeの拡張機能

[Claude Code for VSCode](https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code)

## はじめに `/init` コマンドで`CLAUDE.md`作成

Claude Codeは、一度終了すると内容がリセットされる  
継続させたい場合は`CLAUDE.md`に保存する

```bash
# CLAUDE.md 作成
/init
```

## ルールの設定方法

1. プロジェクト内だけで適用するルール
2. PC全体で共有してほしいルール
3. スコープによって設定するルール

[Claude Codeの「すぐルール忘れる問題」を解決する超効果的な方法を見つけた気がする](https://zenn.dev/sesere/articles/0420ecec9526dc)

## hooks

トリガーが発火すると何かさせたいときに使う  
ex) 作業が終わったら通知させる

**ただし、セキュリティ的に危ないこともできるので注意！！**

## カスタムコマンド

下記フォルダを作成する

```bash
.claude/commands
```

コマンド(プロンプト)ファイルを作る

```bash
optimized.md
```

Claudeコマンドで実行

```bash
/project:optimize
```

## MCPの設定

MCPエラーをデバッグモードで確認

```bash
claude --mcp-debug
```

### 全体に設定

#### VSCode
`C:\Users\%USERPROFILE%\AppData\Roaming\Code\User\mcp.json`

#### Claude Code
`C:\Users\%USERPROFILE%\.claude.json`

### プロジェクト毎個別に設定

#### VSCode
フォルダ内に`.vscode\mcp.json`を新規作成してMCPの設定を書く

テンプレート

```json
{
    "servers": {

    }
}
```

#### Claude Code
フォルダ内に`.mcp.json`を新規作成してMCPの設定を書く

テンプレート  
※少し設定が必要

ファイル : `.claude/settings.local.json`

下記を追加

```json
"enableAllProjectMcpServers": true,
```

ファイル : `.mcp.json`

```json
{
    "mcpServers": {

    }
}
```

## Context7 + Serena + Cipher

[Claude CodeでMCPツール（Context7、Serena、Cipher）を活用してAIコーディングを次のレベルへ](https://qiita.com/sukimaengineer/items/845ad14a3ec2d3c39930)

[Claude Code で Context7、Serena、Cipher を同時使用する際の注意事項](https://qiita.com/sukimaengineer/items/9a0a10d23c86f2a2e850)

[Claude Code を更に賢く - serena と cipher を mcp で使う](https://zenn.dev/sho7650/articles/5d9b46a119a08f)

## Context7

最新ドキュメントの自動取得

### 前提条件

- [Node.js 18+](https://github.com/room202/react?tab=readme-ov-file#volta-%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)

### MCPの設定

コマンドでの追加

```bash
# グローバル設定に追加
claude mcp add -s user context7 -- npx -y @upstash/context7-mcp@latest

# プロジェクト共有設定として追加
claude mcp add -s project context7 -- npx -y @upstash/context7-mcp@latest
```

## Serena

セマンティックコード解析

[AIコーディングの常識が変わる！Claudeを"覚醒"させる知性、「Serena」徹底解説](https://note.com/kyutaro15/n/n61a8825fe303)

[Claude Codeを10倍賢くする無料ツール「Serena」の威力とトークン効率化術](https://zenn.dev/sc30gsw/articles/ff81891959aaef)

[Serena有効化でClaude Code起動時にWebに飛ばされるのをやめる](https://zenn.dev/soramarjr/articles/c0210f128a4d2a)

### 前提条件

- Python

```bash
pip install uv
```

### MCPの設定

コマンドでの追加

```bash
# グローバル設定に追加
claude mcp add -s user serena -- uvx --from git+https://github.com/oraios/serena serena-mcp-server --context ide-assistant  --enable-web-dashboard false --project $(pwd)

# プロジェクト共有設定として追加
claude mcp add -s project serena -- uvx --from git+https://github.com/oraios/serena serena-mcp-server --context ide-assistant  --enable-web-dashboard false --project $(pwd)
```

### 初期化コマンド

```bash
/mcp__serena__initial_instructions
```

## Claude Code よく使うコマンド一覧

※ 危険 : 権限確認をスキップする秘伝のコマンド

```bash
claude --dangerously-skip-permissions
```

考えさせる、深く考えさせる

Claude Code実行中のコマンド欄に下記を入力

```bash
think <プロンプト>
think hard <プロンプト>
ultrathink <プロンプト>
```

### モード切り替え

| コマンド | モード | 説明　|
|---------|------|------|
| `Shift + Tab` x 1  | 自動許可モード | 明示的に許可されていたり、一度許可されたコマンドは自動で許可するモード
| `Shift + Tab` x 2  | プランモード | ファイルを編集せずに、Readonlyで設計を練る |

### ファイル操作

| コマンド | 説明 | 使用例 |
|---------|------|--------|
| `claude --file <filepath>` | 特定のファイルを指定して質問 | `claude --file main.py "このコードをレビューして"` |
| `claude --files <pattern>` | 複数ファイルを指定 | `claude --files "*.js" "全てのJSファイルを最適化して"` |
| `claude --directory <path>` | ディレクトリ全体を対象 | `claude --directory ./src "プロジェクト構造を分析して"` |

### 出力制御

| コマンド | 説明 | 使用例 |
|---------|------|--------|
| `claude --output <filepath>` | 出力をファイルに保存 | `claude --output result.md "READMEを作成して"` |
| `claude --no-stream` | ストリーミング出力を無効化 | `claude --no-stream "コードを生成して"` |
| `claude --quiet` | 静音モード | `claude --quiet --file app.js "バグを修正して"` |

### 設定・認証

| コマンド | 説明 | 使用例 |
|---------|------|--------|
| `claude auth` | 認証設定 | `claude auth` |
| `claude config` | 設定確認・変更 | `claude config` |
| `claude config set model claude-sonnet-4` | 使用モデル設定 | `claude config set model claude-sonnet-4` |

### プロジェクト管理

| コマンド | 説明 | 使用例 |
|---------|------|--------|
| `claude init` | プロジェクトの初期化 | `claude init` |
| `claude status` | プロジェクト状態確認 | `claude status` |
| `claude history` | 対話履歴表示 | `claude history` |

### 便利なオプション

| オプション | 説明 | 使用例 |
|-----------|------|--------|
| `--model` | 使用するモデルを指定 | `claude --model claude-sonnet-4 "コードレビュー"` |
| `--context` | コンテキストファイルを指定 | `claude --context requirements.txt "実装して"` |
| `--interactive` | 対話モード | `claude --interactive` |
| `--json` | JSON形式で出力 | `claude --json "APIレスポンス例を作成"` |

### 実用的な使用パターン

| 用途 | コマンド例 |
|------|-----------|
| コードレビュー | `claude --file app.py "このコードの問題点を指摘して改善案を提示して"` |
| バグ修正 | `claude --files "*.js" "TypeScriptのエラーを修正して"` |
| ドキュメント生成 | `claude --directory ./src --output README.md "READMEを生成して"` |
| テストコード作成 | `claude --file utils.js "ユニットテストを作成して"` |
| リファクタリング | `claude --file legacy.py "モダンなPythonコードにリファクタリングして"` |

## 参考リンク

[公式サイト](https://docs.anthropic.com/ja/docs/claude-code/overview)

[公式リポジトリ](https://github.com/anthropics/claude-code)

[これ読めばOK。私が使ってるものだけの、Claude Code チュートリアル](https://zenn.dev/pepabo/articles/898cdc4839acb8)

[速習 Claude Code](https://zenn.dev/mizchi/articles/claude-code-cheatsheet)

## Pending

GitHubとの連携はさせたが使い方までは未調査

[GitGuardian](https://docs.gitguardian.com/internal-monitoring/integrate-sources/vcs-integrations/github)

以下、OpenAIのAPIを使用するため保留

CodeRabbitの導入  
[もう初回コードレビューはAIに任せる時代になった - CodeRabbit -](https://zenn.dev/minedia/articles/7928ef7545b393)

Cipherの導入