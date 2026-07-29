---
created: 2026-07-29
tags: [RAG, RAGFusion, LLM]
aliases: []
source: https://weel.co.jp/media/tech/ragfusion/
---

# RAG Fusionとは

> 出典: [RAG Fusion: LLMのハルシネーション防止技術 | WEEL](https://weel.co.jp/media/tech/ragfusion/)

## 概要

RAG Fusionは、大規模言語モデル（LLM）の誤回答（ハルシネーション）を防ぐ技術で、従来のRAG（検索拡張生成）の進化版。
「1つの質問を複数のクエリに言い換えて検索し、結果を『RRF』でリランク統合してから回答する」という仕組みを採用している。

## 基本的な仕組み

従来型RAGは質問を直接検索していたが、RAG Fusionでは以下のステップを踏む。

1. ユーザーが質問を入力
2. LLMが関連する新たな質問を複数生成
3. 全てのクエリでベクトルデータベースを検索
4. Reciprocal Rank Fusion（RRF）で検索結果を順位付け統合
5. 上位結果をプロンプトに反映して回答生成

RRFの計算式は「**fused_scores[doc_str] += 1 / (rank + k)**」で、絶対値ではなく順位のみを評価する。

## メリット

- 専門分野でも深い回答が得られる
- あいまいな表現やタイプミスを追加質問で補完
- より正確かつ包括的な検索結果の実現

## デメリット

- トークン消費が増加
- 回答速度が低下
- 質問から外れた回答が返される可能性

## 関連技術との関係

- **Self-RAG**: モデルが自律的に必要な情報を検索
- **GraphRAG**: 知識グラフで複雑な関係性を可視化
- **Agentic RAG**: AIが検索の必要性や方法を自動判断

RAG Fusionは「検索の広げ方」、GraphRAGは「関係性のつなぎ方」、Agentic RAGは「検索の意思決定」を
それぞれ強化する補完的な手法。

## 関連

- [[GraphRAGとは]]
- [[RAGとは]]
