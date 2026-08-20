---
created: 2026-08-20
tags: [Qwen, ローカルLLM, LLM, GPU, Ollama, KVキャッシュ]
aliases: []
source: https://qiita.com/h-nabata/items/390b3558be49c30f85a7
---

# Qwen3.8-27Bの推論性能をテストする WSL2+Ollama+RTX5070Ti

> 出典: [【ローカルLLM】Qwen3.8-27Bの推論性能をテストする（WSL2 + Ollama + RTX 5070 Ti） | Qiita](https://qiita.com/h-nabata/items/390b3558be49c30f85a7)

## 概要

著者がOllamaを用いてQwen3.8-27BモデルをローカルPC環境で実行し、推論性能・設定方法・
応用例（数学・化学）を検証したレポート。

## 使用技術・ツール

| 項目 | 仕様 |
|------|------|
| GPU | NVIDIA GeForce RTX 5070 Ti（VRAM 16GB） |
| CPU | AMD Ryzen 7 5800X3D（8コア/16スレッド） |
| メモリ | 64GB（WSL2に48GB割り当て） |
| OS | Windows 26200、WSL2（Ubuntu 24.04） |
| LLMフレームワーク | Ollama 0.32.13 |
| モデル | Qwen3.8-27B（Q4_K_M量子化） |

## 環境設定・手順

### 1. WSL2メモリ割り当て拡張
`C:\Users\<user>\.wslconfig` に以下を記述。
```
[wsl2]
memory=48GB
swap=8GB

[experimental]
autoMemoryReclaim=gradual
```

### 2. Ollama量子化KVキャッシュ設定
`/etc/systemd/system/ollama.service.d/override.conf` に以下を追加。
```
[Service]
Environment="OLLAMA_KV_CACHE_TYPE=q8_0"
Environment="OLLAMA_FLASH_ATTENTION=1"
Environment="OLLAMA_KEEP_ALIVE=1h"
```

### 3. コンテキスト長変更
Ollama CLI実行時に `/set parameter num_ctx 16384` を実行。

## 推論テスト結果

### 正答事例
- 2元1次連立方程式: 正確に x=32/7, y=-3/7 を導出
- 平方数の和の公式: n(n+1)(2n+1)/6 を証明（テレスコープ法）
- 3次方程式の解: 有理根定理を用い、実根1つと複素根2つを正確に算出
- 化学量論計算: HClを制限反応成分と判定、CO2生成量3.30gを正答
- 有機反応機構: 2-ブロモブタンのNaCN/DMSO反応をSN2と判定、KOtBu条件をE2と判定しHofmann則でプロダクトを予測

### 誤答・弱点
- 南極観測基地: 実在する「みずほ基地」「あすか基地」を認識できず、昭和基地とドームふじ基地のみを列挙
- 大谷翔平の経歴: 誤った所属・入団年・MVP受賞履歴を記述（阪神入団と誤記載など）
- Gaussian 16入力生成: キーワード体系の混同、分子座標の幾何学的不整合が発生

## 考察・結論

「Thinking」モードの有効活用が重要。著者は推論強度を用途に応じて調整することを推奨。
- 単純質問ではThinking OFF
- 通常の推論では強度をlow〜mediumに
- 複雑問題でのみ強いThinking使用

自然言語ベースの化学推論（量子化学、反応機構、電子論）では性能が高い一方、事実知識の幻覚や
計算化学ソフトウェア固有の入力生成では限界がある。実用的なエージェント構築には、LLMに自然言語解釈を
任せ、ツール固有の厳密性が必要な部分（座標生成、キーワード検証など）は決定論的プログラムに分担させる
べきと指摘。RTX 5070 Ti 16GBでの運用は実現可能だが、CPUオフロード発生時の速度低下を考慮が必要。

## 関連

- [[Qwen3.8-27BをRX6800で動かしてローカルモデルを比較]] — 同じQwen3.8-27Bのローカル実行検証。VRAM 16GB帯というハードウェア条件が共通
- [[Qwen3.8-27BをRTX5090で実測 ローカルLLM5モデル徹底比較]] — 同じQwen3.8-27Bの実測レポートで、上位GPU（RTX5090）との速度・VRAM使用量の比較対象になる
- [[TransformerのKVキャッシュを用いたDecode処理を理解する]] — 本記事で設定しているOLLAMA_KV_CACHE_TYPE（量子化KVキャッシュ）が、KVキャッシュのメモリ課題への実践的な対処法にあたる
- [[OllamaをAgentic RAGのバックエンドにする]] — LLMに自然言語解釈を任せ厳密な処理は決定論的プログラムに分担させるという指摘が、ツール呼び出しによるハルシネーション対策という考え方と共通
