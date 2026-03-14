# LangChain RAG Building Blocks

This repository contains the **core building blocks required to build Retrieval-Augmented Generation (RAG) systems using LangChain**.

The goal of this repository is to understand each component of the RAG pipeline step by step, including **data ingestion, text transformation, embeddings, and vector databases**.

---

## RAG Architecture

Typical RAG workflow:

Documents  
↓  
Document Loaders  
↓  
Text Splitters  
↓  
Embeddings  
↓  
Vector Database  
↓  
Retriever  
↓  
Large Language Model (LLM)

Each folder in this repository focuses on **one component of the RAG pipeline**.

---

# Repository Structure
## Repository Structure

```
langchain-rag-building-blocks
├── 0-rag-concepts
│   ├── why_rag_is_needed.md
│   ├── rag_pipeline_explanation.md
│   └── retrievers.md
│
├── 1-data-ingestion
│   ├── data-ingestion.ipynb
│   └── document_loader_notes.md
│
├── 2-data-transformer
│   ├── 1-CharacterTextsplitter.ipynb
│   ├── 2-RecuriveCharactertextsplitter.ipynb
│   ├── 3-HTMLtextsplitter.ipynb
│   ├── 4-RecursiveJsonSplitter.ipynb
│   └── langchain_text_splitters_notes.md
│
├── 3-embeddings
│   ├── 1-embedding.ipynb
│   ├── 2-ollamaembedding.ipynb
│   ├── 3-huggingface.ipynb
│   └── langchain_embeddings_notes.md
│
├── 4-vector-stores
│   ├── 1-faiss-vectorstore.ipynb
│   ├── 2-chroma-vectorstore.ipynb
│   └── langchain_vectorstores_notes.md
│
├── data
│   ├── attention.pdf
│   ├── records.xml
│   └── speech.txt
│
├── requirements.txt
└── README.md
```


---

# Concepts Covered

### 1️⃣ RAG Fundamentals
- Why RAG is needed  
- RAG pipeline architecture  
- Retrievers and document retrieval  

### 2️⃣ Data Ingestion
- Document loaders  
- Loading data from TXT, PDF, and XML files  

### 3️⃣ Data Transformation
- CharacterTextSplitter  
- RecursiveCharacterTextSplitter  
- HTMLHeaderTextSplitter  
- RecursiveJsonSplitter  

### 4️⃣ Embeddings
- OpenAI embeddings  
- HuggingFace embeddings  
- Ollama embeddings  

### 5️⃣ Vector Databases
- FAISS vector store  
- Chroma vector store  
- Similarity search  

---

# Technologies Used

- Python  
- LangChain  
- HuggingFace  
- Ollama  
- FAISS  
- Chroma  

---

# Purpose of This Repository

This repository is created to **deeply understand the internal components of RAG systems** before building full GenAI applications.

It focuses on learning:

- How documents are loaded  
- How text is split  
- How embeddings are generated  
- How vector databases store embeddings  
- How retrievers fetch relevant documents  

---

# Future Work

Next steps after these building blocks:

- Implement a **complete RAG pipeline**
- Build **RAG applications using OpenAI / Ollama**
- Add **LangChain Chains and Agents**

---

# Author

**Shaik Zaid**