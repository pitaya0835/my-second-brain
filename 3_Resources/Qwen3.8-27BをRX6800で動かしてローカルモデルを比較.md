---
created: 2026-08-20
tags: [Qwen, ローカルLLM, LLM, GPU, ベンチマーク]
aliases: []
source: https://zenn.dev/omohikane/articles/qwen38-test-my-rx6800
---

# Qwen3.8-27BをRX6800で動かしてローカルモデルを比較

> 出典: [Qwen3.8-27BをRX6800 16GBで動かしてローカルモデルを比較してみた | Zenn](https://zenn.dev/omohikane/articles/qwen38-test-my-rx6800)

## 概要

著者が自宅のAMD RX6800（VRAM 16GB）でQwen3.8-27Bを含む複数のローカルLLMを実行し、
「~/.config/nvim の構成を説明する」という単一タスクで性能を比較した実験レポート。
厳密なベンチマークではなく実用性の検証が目的。

## 検証環境

- GPU: AMD Radeon RX 6800（VRAM 16GB）
- フレームワーク: llama.cpp Vulkan + litellm
- タスク: 「~/.config/nvim の構成を説明する」（単一問題での評価、新規セッション）

## 検証対象モデル

1. Qwen3.8-27B（Q3_K_M、UD-Q2_K_XL）
2. gpt-oss-20B（MXFP4）
3. North Mini Code（MoE 30B/3B）
4. G4-MeroMero-26B（IQ4_XS、Gemma4系）
5. Devstral-24B
6. Qwen3.6-27B-Fable（IQ3_M）
7. DeepSeek Flash（API参照用）

## 主要結果

| モデル | 実行時間 | 生成速度 | 評価 |
|--------|---------|---------|------|
| G4-MeroMero-26B | 2m55s | 最速 | 詳細度・速度ともトップ |
| Qwen3.8-27B Q2_K_XL | 4m35s | 29.3 t/s | 品質高い、CTX長い |
| Qwen3.8-27B Q3_K_M | 3m55s | 12.7 t/s | 安定だが遅い |
| Qwen3.6-Fable | 計測不能 | 11.5 t/s | プロンプト処理が遅い |

## 手順

各モデルでOpenCode（エージェント）を使用し、find/Glob/Readなどのツール連鎖を通じて
設定ファイルを調査させ、最終的な説明の正確さと速度を計測。

## 考察・結論

- **日常利用の第一候補: G4-MeroMero-26B** — 最速完走（2m55s）、詳細度もローカルモデル中トップ。
  弱点はCTX長が短くVRAM余裕がほぼない点。
- **長文・エージェント長期実行: Qwen3.8-27B（UD-Q2_K_XL）** — CTXが32768と長く、VRAM余裕約3GB確保。
  品質はQ3_K_M並みで生成速度は約2倍。
- その他の課題: Devstral-24Bはopencodeのchat template制約により実用不可、Qwen3.6-Fableはプロンプト処理が遅くターン進行が追いつかない、gpt-oss-20Bはツール結果の解釈が不正確。
- 結論として、ローカルモデル選択は単一タスクではなく実際の使用パターン次第。日常タスクはMero、長文エージェントではQwen3.8 Q2_K_XLという使い分けを提案。

## 関連

- [[Qwen-MM-PluginsによるAIエージェントのマルチモーダル拡張]] — 同じQwen系モデル・AIエージェント文脈という点で関連
- [[OllamaをAgentic RAGのバックエンドにする]] — ローカルLLMをエージェントのバックエンドとして運用する際のモデル選定（VRAM・量子化・速度のトレードオフ）という論点が共通
