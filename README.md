# **RAG with Gemini API ✧**

## Overview
This project explores Retrieval-Augmented Generation (RAG) using Google’s Gemini LLMs with different embedding models and configurations. The goal is to evaluate how varying chunking strategies, embedding models, and retrieval settings affect the performance of RAG pipelines.  

The main notebook walks through the process of building, configuring, and testing RAG systems, while the accompanying JSON configuration files define experimental setups.

## Key Learnings

### 1. Effect of Chunk Size and Overlap
- Two chunking strategies were tested:  
  - 300 tokens with 50 overlap  
  - 500 tokens with 100 overlap  
- Smaller chunks (300/50) provide more granular retrieval, which may improve accuracy for fine-grained queries.  
- Larger chunks (500/100) reduce retrieval calls but risk including unnecessary text, potentially leading to less precise answers.  

### 2. Embedding Model Comparison
  - `intfloat/e5-small-v2`  
  - `sentence-transformers/all-MiniLM-L6-v2`  

Findings:  
- e5-small-v2 is optimized for semantic search and often produces stronger retrieval relevance.  
- MiniLM is lightweight and faster, but retrieval quality may vary depending on the dataset and query complexity.  

### 3. LLM Integration with Gemini
- All configurations use Gemini-2.5-Flash as the reasoning model.  
- The pipeline demonstrates how Gemini leverages external retrieved knowledge to enhance factual accuracy, especially in domain-specific contexts.  

### 4. Retriever Parameters
- `retriever_k=4` across all configs ensures the model retrieves the top 4 most relevant chunks.  
- Balancing `k` is crucial:  
  - Higher `k` provides broader context, but risks adding noise.  
  - Lower `k` offers concise retrieval, but may miss important evidence.  

## Key Learnings

### Chunk Size
- Small chunks (300 tokens, 50 overlap) improve precision by isolating information more clearly, making retrieval highly accurate for specific queries.  
- Large chunks (500 tokens, 100 overlap) improve efficiency by reducing retrieval calls, but risk introducing irrelevant context.  
- The right chunk size balances accuracy and efficiency depending on the task.  

### Embeddings
- `e5-small-v2` provides stronger semantic search and more relevant retrievals.  
- `MiniLM` is faster and lighter but less consistent for nuanced queries.  
- Embedding quality directly determines whether the LLM gets the right evidence to work with.  

### Why They Matter
Chunking and embeddings are the foundation of RAG. Poor chunking limits what embeddings can capture, and weak embeddings reduce the value of even well-chosen chunks. Together, they decide whether the LLM reasons over useful, accurate context.

## Takeaways
- Smaller chunks = higher precision; larger chunks = more efficiency.  
- Stronger embeddings = better grounding and more accurate answers.  
- The effectiveness of RAG depends on tuning both together.  
