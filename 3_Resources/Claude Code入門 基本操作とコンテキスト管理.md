---
created: 2026-08-06
tags: [Claude Code, AIエージェント, LLM, ハーネス]
aliases: []
source: https://zenn.dev/cscloud_blog/articles/csc-claude-code-study-session-02
---

# Claude Code入門 #2 — 基本操作とコンテキスト管理

> 出典: [\[社内勉強会資料公開\] Claude Code 入門 #2 — 基本操作とコンテキスト管理 | Zenn](https://zenn.dev/cscloud_blog/articles/csc-claude-code-study-session-02)

## 概要

サイバーセキュリティクラウド社内の勉強会資料第2回。
日常業務での基本コマンドとコンテキスト管理、Permission Mode（権限設定）の活用法に焦点を当てている。
[[Claude Code入門 AIエージェントの仕組みとセットアップ]]（#1）の続編。

## 3行まとめ（記事掲載）

- コンテキストには上限があり、埋まるほど応答精度が低下する。`/context`で残量確認、`/compact`で要約が基本
- Permission Modeを`Shift+Tab`で切り替え、影響の大きい作業は計画モードで確認する
- ファイル変更はいつでも`/rewind`で巻き戻せるため、積極的に試行できる

## コンテキストの概念

「これまでの会話内容が次のやり取りに引き継がれる情報」として定義。上限に達するとパフォーマンス低下が発生する。

## スラッシュコマンド4種

- `/help`: 利用可能コマンド表示
- `/clear`: 会話リセット
- `/compact`: 会話要約によるコンテキスト最適化
- `/context`: 使用状況可視化

## Permission Mode（4段階）

- **Default**: 毎回確認要求
- **Auto-accept edits**: 基本操作は自動実行
- **Plan mode**: 計画のみ提示
- **Auto mode**: ほぼ全操作を自動実行（実験段階）

## その他の機能

- `/btw`: 本筋と無関係な質問用
- 画像貼り付けと`@`ファイル参照
- チェックポイント機能（`/rewind`または`Esc`2回）

## ミニハンズオン

4つの実践手順で、各機能（コンテキスト確認、Permission Mode切り替え、rewind等）を体験できる構成。

## 扱われているトピック

- Claude Codeの基本的な使い方
- コンテキスト管理戦略
- 権限設定モードの使い分け
- ファイル編集時の安全性機能
- チーム内での共有・運用方法（次回予定の`CLAUDE.md`）

## 関連

- [[Claude Code入門 AIエージェントの仕組みとセットアップ]] — 同シリーズ第1回
- [[OllamaをAgentic RAGのバックエンドにする]] — agentic loopやセッション管理の考え方が共通
