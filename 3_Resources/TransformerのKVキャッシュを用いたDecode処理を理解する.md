---
created: 2026-08-20
tags: [Transformer, LLM, KVキャッシュ, Attention, 推論]
aliases: []
source: https://qiita.com/kenmatsu4/items/3126a7ff8d626f220202
---

# TransformerのKVキャッシュを用いたDecode処理を理解する

> 出典: [TransformerのKVキャッシュを用いたDecode処理を理解する | Qiita](https://qiita.com/kenmatsu4/items/3126a7ff8d626f220202)

## 概要

Transformer推論における2段階のプロセス（Prefill・Decode）を解説し、特にKVキャッシュが
Decode段階で計算効率を飛躍的に向上させるメカニズムを図解で説明している記事。

## 扱っている技術

- Transformerアーキテクチャ
- Multi-Head Attention機構
- KVキャッシュ（Key-Value Cache）
- 自己回帰生成（Auto-regressive Generation）
- Causal Masking

## 手順・仕組み

**1段階目: Prefill**
入力プロンプト全体を並列処理し、K・Vを計算してキャッシュに保存する。

**2段階目: Decode**
以下を繰り返す。
- 新規トークンのQ・K・Vベクトルのみ計算
- 過去のK・Vはキャッシュから再利用
- 新規K・Vをキャッシュに追加連結
- Attention計算で次トークンを生成

## 具体例

「[BOS] two kids are playing...」というプロンプトの後、次トークンが"Then"になるケースで説明。
n個のトークン処理後、n+1番目のトークンの q_{n+1}, k_{n+1}, v_{n+1} ベクトルのみを計算することで
効率化を実現している。

## 結論

キャッシュされたK・Vがあれば、以降は新規トークンのベクトルのみで次トークンの出力が可能となり、
極めて効率的。ただしコンテキストウィンドウの増大に伴うメモリ課題（KVキャッシュのメモリ使用量増大）が存在する。

## 関連

- [[Qwen3.8-27BをRX6800で動かしてローカルモデルを比較]] — 記事内で言及されるCTX長（コンテキストウィンドウ）とVRAM消費のトレードオフは、本記事のKVキャッシュのメモリ課題そのものが原因
- [[OllamaをAgentic RAGのバックエンドにする]] — コンテキスト長制約への対応という運用課題が、本記事のKVキャッシュのメモリ肥大化という技術的背景と対応する
- [[Qwen3.8-27Bの推論性能をテストする WSL2+Ollama+RTX5070Ti]] — OLLAMA_KV_CACHE_TYPE=q8_0によるKVキャッシュの量子化という、本記事の技術を実践に応用した具体例
