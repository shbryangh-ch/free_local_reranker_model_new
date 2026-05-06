# free_local_reranker_model_new
在本地環境部署免費開源的 reranker 模型（例如 BAAI/bge-reranker-large），透過 FastAPI 建立自有 API 服務，實現文件重排序（reranking）功能。此方式可避免依賴第三方 API，消除請求次數限制與額外費用，同時提升資料隱私性與系統回應速度，適合用於 RAG（Retrieval-Augmented Generation）架構中的檢索優化。
