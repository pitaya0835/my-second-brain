---
created: 2026-08-06
tags: [Claude Code, AIエージェント, LLM, ハーネス, セキュリティ]
aliases: []
source: https://zenn.dev/cscloud_blog/articles/csc-claude-code-study-session-04
---

# Claude Code入門 #4 — permissions・hooks・devcontainerで安全に使う

> 出典: [\[社内勉強会資料公開\] Claude Code 入門 #4 — permissions・hooks・devcontainerで安全に使う | Zenn](https://zenn.dev/cscloud_blog/articles/csc-claude-code-study-session-04)

## 概要

サイバーセキュリティクラウド社内の勉強会資料第4回。
Claude Codeを安全に運用するための設定・仕組み（permissions、hooks、DevContainer）を扱う。
[[Claude Code入門 CLAUDE.mdとメモリで自分仕様にする]]（#3）の続編。

## 主な論点：安全運用の3段階アプローチ

1. **抑止**: CLAUDE.mdで危険行動を指示段階で防止
2. **制限**: permissions設定とhooksで技術的に操作範囲を絞込
3. **隔離**: DevContainerで影響範囲を環境ごと分離

## 扱われている技術・ツール

- `settings.json`内のpermissions設定
- Hooksによるライフサイクルイベント処理
- DevContainer（VS Code機能）
- 組み込みsandboxモード
- MCP（Model Context Protocol）サーバー

## 具体的な手順・設定例

「読み取り・調査系のコマンドは自動実行してよいが、書き込みや外部通信を伴う操作は必ず人間が確認する」という運用を基本形として推奨。
ls・find・grep・catなどのコマンドのみを許可するサンプル設定を提示している。

## 結論

セキュリティコンサルタント業務で顧客機密情報を扱う場合、事前の契約確認、最小限の権限から始める段階的アプローチ、
および信頼できない情報源の隔離環境処理が必須とされている。

## 関連

- [[Claude Code入門 CLAUDE.mdとメモリで自分仕様にする]] — 同シリーズ第3回
- [[Claude Code入門 基本操作とコンテキスト管理]] — 同シリーズ第2回
- [[Claude Code入門 AIエージェントの仕組みとセットアップ]] — 同シリーズ第1回
- [[OllamaをAgentic RAGのバックエンドにする]] — agentic loopやセッション管理の考え方が共通
- [[Qwen-MM-PluginsによるAIエージェントのマルチモーダル拡張]] — MCP（Model Context Protocol）サーバーの活用という点で技術的に関連
