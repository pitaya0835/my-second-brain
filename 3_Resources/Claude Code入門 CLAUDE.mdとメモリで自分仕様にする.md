---
created: 2026-08-06
tags: [Claude Code, AIエージェント, LLM, ハーネス]
aliases: []
source: https://zenn.dev/cscloud_blog/articles/csc-claude-code-study-session-03
---

# Claude Code入門 #3 — CLAUDE.mdとメモリで自分仕様にする

> 出典: [\[社内勉強会資料公開\] Claude Code 入門 #3 — CLAUDE.mdとメモリで自分仕様にする | Zenn](https://zenn.dev/cscloud_blog/articles/csc-claude-code-study-session-03)

## 概要

サイバーセキュリティクラウド社内の勉強会資料第3回。
CLAUDE.mdとAuto Memory機能を使ってClaude Codeを自分・チーム仕様にカスタマイズする方法を扱う。
[[Claude Code入門 基本操作とコンテキスト管理]]（#2）の続編。

## CLAUDE.mdの役割

作業フォルダに置くだけでClaude Codeが毎回自動的に読み込む「自己紹介と業務マニュアル」として機能する。
毎回同じ指示を繰り返す非効率性を解消するツール。

## スコープ（適用範囲）の4階層

- **Managed**: 組織全体
- **User**: 個人全体。`~/.claude/CLAUDE.md`に配置
- **Project**: プロジェクト。作業フォルダ直下
- **Local**: 個人・当該プロジェクトのみ。`CLAUDE.local.md`で共有外の情報を管理

## 具体的な手順

1. **初期化コマンド**: `/init`を使用してClaude Code自身が下書きを自動生成
2. **ファイル作成**: 作業フォルダに`CLAUDE.md`を作成し、具体的で測定可能なルールを記載
3. **確認方法**: プロジェクトのルール内容について質問し、正しく読み込まれているか検証

## 技術的なポイント

- Auto Memory機能により、Claude Codeが会話から学んだ経験則が自動記録される
- CLAUDE.mdは「人間が書く指示書」、Auto Memoryは「AIが学習する経験則」と区別される
- 「必ず守ること」「できれば守ってほしいこと」と優先度を明示することが推奨される

## 結論

CLAUDE.mdは一度作成して終わりではなく、実務を通じて継続的に育成していくもの。
チーム全体で共有することで、個人の気づきをチーム資産に変換できる。

## 関連

- [[Claude Code入門 基本操作とコンテキスト管理]] — 同シリーズ第2回
- [[Claude Code入門 AIエージェントの仕組みとセットアップ]] — 同シリーズ第1回
- [[OllamaをAgentic RAGのバックエンドにする]] — agentic loopやセッション管理の考え方が共通
