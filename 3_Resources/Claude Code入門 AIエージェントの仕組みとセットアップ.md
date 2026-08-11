---
created: 2026-08-06
tags: [Claude Code, AIエージェント, LLM, ハーネス]
aliases: []
source: https://zenn.dev/cscloud_blog/articles/csc-claude-code-study-session-01
---

# Claude Code入門 #1 — AIエージェントの仕組みとセットアップ

> 出典: [\[社内勉強会資料公開\] Claude Code 入門 #1 — AI エージェントの仕組みとセットアップ | Zenn](https://zenn.dev/cscloud_blog/articles/csc-claude-code-study-session-01)

## 概要

サイバーセキュリティクラウド社の技術アカウントマネージャー向け社内勉強会資料を公開した記事。
Claude Codeの基礎理解・セットアップ・初回体験までを扱う第1回。

## Claude Codeの本質

Claude Codeは「ハーネス」であると定義されている。
「Claude CodeはLLMであるClaudeそのものではなく、LLMを実際の作業に使えるようにする『ハーネス』」という説明で、
単なるモデルではなく実行基盤であることを強調している。

### 3つの構成要素

- **ツール**: ファイル操作、コマンド実行など
- **agentic loop**: 思考→実行→確認の反復
- **状態管理**: コンテキスト保持

### 2層構造

内部ハーネス（既備機能）と外部ハーネス（ユーザーカスタマイズ層）を区別し、実装段階を明確化している。

## セキュリティコンサルティングとの関連性

AIペネトレーションテストツール「XBOW」がHackerOneで人間を上回った事例を引き、実務活用の重要性を提示している。

## セットアップ手順

- macOS/Linux/WSL向けコマンド
- Windows PowerShell手順
- 3つのログイン方式（Claude Pro、API、クラウド統合）

### よくあるトラブルシューティング

- WSL環境での混同
- 社内プロキシ対応
- ブラウザ認証画面の問題

## 実践ハンズオン

初心者向けに「メモ要約」という非プログラミング業務からagentic loopを体験させる設計になっている。

## ベストプラクティス

具体的かつ明確な指示の重要性を強調し、曖昧な依頼と具体的な依頼の対比を示している。

## 関連

- [[OllamaをAgentic RAGのバックエンドにする]] — agentic loop（応答→ツール実行→結果フィードバックの循環）の考え方が共通
- [[Claude Code入門 基本操作とコンテキスト管理]] — 同シリーズ第2回
- [[Qwen-MM-PluginsによるAIエージェントのマルチモーダル拡張]] — Claude Codeが「ハーネス」であるという定義が、Qwen-MM-Pluginsの「エージェントハーネス層」という考え方と共通
