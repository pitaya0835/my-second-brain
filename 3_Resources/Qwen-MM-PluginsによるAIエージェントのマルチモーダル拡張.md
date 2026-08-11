---
created: 2026-08-11
tags: [Qwen, AIエージェント, マルチモーダル, MCP, ハーネス]
aliases: []
source: https://weel.co.jp/media/tech/qwen-mm-plugins/#index_id0
---

# Qwen-MM-PluginsによるAIエージェントのマルチモーダル拡張

> 出典: [【Qwen-MM-Plugins】AIエージェントにマルチモーダル能力を追加！仕組み・使い方・活用シーンを徹底解説 | WEEL](https://weel.co.jp/media/tech/qwen-mm-plugins/#index_id0)

## 概要

Alibaba Cloudが2026年8月に公開した拡張ライブラリ。「テキストベースのエージェントに目と手を与える」ツールと位置づけられ、
既存のAIコーディングエージェント（Claude Code、Codex、Qwen Code、Gemini CLIなど）に画像・動画・3D・CAD処理機能を
後付けで追加できる。

## 主要特徴

- 6種類の独立したケイパビリティ（core、video-memory、video-edit、blender、freecad、edu-agent）
- ハーネス横断的な互換性（Claude Codeなど複数のエージェントハーネスで利用可能）
- Apache License 2.0のオープンソース、ライブラリ自体は無料利用可能

## 技術アーキテクチャ

3層構造になっている。

1. エージェントハーネス層
2. Skill＋MCPサーバー層
3. バックエンドAPI/ローカルツール層

## 仕組み

モジュラー設計とダイナミックレゾリューション方式を採用。

## 特徴（インストール・互換性）

粒度の細かいインストールが可能で、必要なケイパビリティのみを選んで導入できる。

## 安全性・制約

APIキーが必要で、Windows環境では一部機能に制限がある。

## 料金

DashScope APIなど、使用するバックエンドサービスに応じた従量課金。

## ライセンス

Apache License 2.0。帰属表記が必要。

## 使い方

インストーラーが用意されており、各ハーネス（Claude Code、Codex、Qwen Code、Gemini CLIなど）ごとの導入手順が
案内されている。

## 活用シーン

- 建築（CAD連携）
- 動画制作
- 研究・教育（edu-agent）

## 実装検証

記事内では画像読み取りとOCRの動作確認例が紹介されている。

## FAQ

よくある質問への回答セクションあり（詳細は出典記事を参照）。

## 関連

- [[Claude Code入門 AIエージェントの仕組みとセットアップ]] — Claude Codeが「ハーネス」であるという定義が、Qwen-MM-Pluginsの「エージェントハーネス層」という考え方と共通
- [[Claude Code入門 permissions・hooks・devcontainerで安全に使う]] — MCP（Model Context Protocol）サーバーの活用という点で技術的に関連
- [[OllamaをAgentic RAGのバックエンドにする]] — 既存のテキストベースAIエージェントにツール呼び出しで能力を拡張するという設計思想が共通
