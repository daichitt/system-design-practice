# モデル出力の最適化（Optimizing model outputs）

## 1. 概要
基盤モデル（FM）のライフサイクルにおいて重要な最適化フェーズでは、コストと複雑さが異なる複数の手法を用いて、モデルの出力を目的に合わせて向上させることができます。その中で**最も速く、かつ低コスト**で行える手法がプロンプトエンジニアリングです。

---

## 2. 主な最適化手法の比較

### プロンプトエンジニアリング（Prompt Engineering）
* **特徴:** モデルの重みを変更せず、指示（プロンプト）の設計や最適化によって望む結果を引き出す手法（コスト・複雑さが最も低い）。
* **主な要素:**
  * **Instructions（指示）:** モデルに実行させるタスクの説明。
  * **Context（コンテキスト）:** モデルを誘導するための外部情報。
  * **Input data（入力データ）:** 処理対象となるデータ。
  * **Output indicator（出力インジケータ）:** 出力のタイプやフォーマットの指定。

#### サンプルプロンプト（Example prompt）
```text
You are an experienced journalist that excels at condensing long articles into concise summaries. Summarize the following text in 2–3 sentences.
Text: [Long article text goes here]