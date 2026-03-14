# LangChain Vector Databases (Vector Stores)

Vector databases are used to **store embeddings and perform similarity search**.

In RAG systems, embeddings of documents are stored inside a vector database.  
When a user asks a question, the question is converted into an embedding and the system searches for the most similar vectors.

The retrieved documents are then sent to the **LLM to generate an answer**.

---

# Why Vector Databases Are Needed

LLMs cannot directly search large document collections.

Problems without vector databases:

- Too many documents to scan  
- Slow retrieval  
- Difficult to find semantically similar content  

Vector databases solve this by:

- storing embeddings  
- performing fast similarity search  
- retrieving relevant documents  

---

# Vector Database Workflow

```
Documents
   ↓
Text Splitter
   ↓
Embeddings
   ↓
Vector Database
   ↓
Retriever
   ↓
LLM
```

Example:

User Question:

```
"What is machine learning?"
```

```
Question → embedding → search vector database
```

The vector database returns the **most relevant document chunks**.

---

# Data Stored in Vector Databases

Vector databases store two main things:

### 1. Embeddings (numerical vectors)

Example:

```
[0.234, -0.112, 0.654, 0.981, ...]
```

### 2. Metadata

Example:

```json
{
  "source": "attention.pdf",
  "page": 2
}
```

---

# Common Vector Databases

LangChain supports many vector databases.

Popular ones include:

- FAISS
- Chroma
- Pinecone
- Weaviate
- Milvus
- Qdrant

---

# FAISS Vector Database

FAISS (**Facebook AI Similarity Search**) is a local vector database.

### Features

- runs locally
- very fast similarity search
- widely used for RAG systems
- no external server required

### Example

```python
from langchain.vectorstores import FAISS

vectorstore = FAISS.from_documents(documents, embeddings)
```

### Save FAISS index

```python
vectorstore.save_local("faiss_index")
```

### Load FAISS index

```python
FAISS.load_local("faiss_index", embeddings)
```

---

# Chroma Vector Database

Chroma is a lightweight vector database designed for AI applications.

### Features

- persistent storage
- easy LangChain integration
- supports metadata filtering
- good for small and medium datasets

### Example

```python
from langchain.vectorstores import Chroma

vectorstore = Chroma.from_documents(
    documents,
    embeddings,
    persist_directory="chroma_db"
)
```

### Persist database

```python
vectorstore.persist()
```

---

# Similarity Search

Vector databases allow **semantic search**.

Example:

```python
results = vectorstore.similarity_search(
    "What is machine learning?"
)
```

Example Output:

```
1. Machine learning is a field of artificial intelligence...
2. Deep learning is a subset of machine learning...
```

These retrieved documents are sent to the **LLM for answer generation**.

---

# Key Idea

Vector databases **store embeddings and allow fast semantic search**.

They are a **core component of Retrieval-Augmented Generation (RAG) systems**.