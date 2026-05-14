# free_local_reranker_model_new
在本地環境部署免費開源的 reranker 模型（例如 BAAI/bge-reranker-large），透過 FastAPI 建立自有 API 服務，實現文件重排序（reranking）功能。此方式可避免依賴第三方 API，消除請求次數限制與額外費用，同時提升資料隱私性與系統回應速度，適合用於 RAG（Retrieval-Augmented Generation）架構中的檢索優化。


# 🚀 Local Reranker API（FastAPI + BGE）部署指南

本專案示範如何在本地部署免費開源 reranker 模型，建立 REST API 服務，取代外部 API 限制，實現零成本、高隱私、低延遲的檢索重排序（Reranking）能力。

---

# 📌 專案目標

在本地環境部署 reranker 模型，並透過 FastAPI 提供 `/rerank` API，使其可用於 RAG（Retrieval-Augmented Generation）流程中，提升檢索結果排序品質。

---

# 🧠 架構概念

```
User Query
    ↓
Retriever（向量檢索）
    ↓
Reranker（本專案）⭐
    ↓
LLM / Answer Generation
```

---

# 🧰 使用技術

* Python 3.10+
* FastAPI
* PyTorch
* HuggingFace Transformers
* BAAI/bge-reranker-large

---

# 📦 安裝環境

## 1️⃣ 建立 Conda 環境（建議）

```bash
conda create -n reranker python=3.10 -y
conda activate reranker
```

---

## 2️⃣ 安裝套件

```bash
pip install fastapi uvicorn transformers torch
```

---

# 🧠 Reranker API 程式碼

在release裡面

---

# 🚀 啟動服務

```bash
python -m uvicorn rerank_server:app --host 0.0.0.0 --port 8001
```

成功後會看到：

```
Uvicorn running on http://0.0.0.0:8001
```

---

# 🧪 API 測試

## Request

```json
POST http://127.0.0.1:8010/rerank #8010可替換成你電腦上目前沒有在用的port

{
  "query": "what is AI",
  "documents": [
    "AI is artificial intelligence",
    "Bananas are yellow",
    "Machine learning is part of AI"
  ],
  "top_n": 2
}
```

---

## Response

```json
{
  "results": [
    {"index": 0, "score": 0.92},
    {"index": 2, "score": 0.88}
  ]
}
```

---

# 🔗 Dify / RAG 整合方式

可將此 API 接到 Dify rerank node：

* URL: `http://your-ip:8001/rerank`
* Method: POST
* Body JSON:

```json
{
  "query": "{{query}}",
  "documents": {{documents}},
  "top_n": 5
}
```

---

# ⚡ 優點

* ❌ 不依賴外部 API
* ❌ 無 token / rate limit
* ❌ 無額外成本
* ✅ 資料不出內網（高隱私）
* ✅ 可自訂模型

---

# 📈 可擴展方向

* GPU 加速推論
* batch reranking
* 多 reranker model 切換（BGE / Qwen / Cross-encoder）
* cache scoring 結果

---

# 🧠 結論

本專案透過本地部署 reranker 模型，將檢索排序能力內建於系統中，適用於企業 RAG、知識庫問答與 AI 檢索優化場景。
