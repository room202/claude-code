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

## `/init` コマンドで`CLAUDE.md`作成

Claude Codeは、一度終了すると内容がリセットされる  
継続させたい場合は`CLAUDE.md`に保存する

```bash
# CLAUDE.md 作成
/init
```

## Claude Code よく使うコマンド一覧

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
