# Retrievers in RAG Systems

## Definition (Interview Level)

A **retriever** is a component that fetches the most relevant documents from a knowledge base (usually a vector database) based on a user query.

In **Retrieval-Augmented Generation (RAG)**, the retriever acts as a bridge between the **vector database** and the **Large Language Model (LLM)**.

Its role is to search the stored embeddings and return the **top relevant document chunks** that will be passed to the LLM as context.

---

## Why Retrievers Are Needed

Vector databases store **thousands or millions of document embeddings**.

When a user asks a question, the system must:

1. Convert the question into an embedding  
2. Search the vector database  
3. Find the most similar embeddings  
4. Retrieve the corresponding documents  

Doing this manually every time can make the system complex.

Retrievers simplify this process by providing a **standard interface for document retrieval**.

---

## Manual Retrieval (Without Retrievers)

Before using retrievers, developers directly queried the vector database.

Example:

```python
results = vectorstore.similarity_search(query, k=3)
```

### Manual Workflow

User Question  
↓  
Convert question → embedding  
↓  
Vector database similarity search  
↓  
Return top-k similar documents  

Example manual code:

```python
query = "What is machine learning?"

results = vectorstore.similarity_search(query, k=3)

for doc in results:
    print(doc.page_content)
```

### Drawbacks of Manual Retrieval

- Different vector databases have different APIs  
- Harder to integrate with RAG pipelines  
- Requires writing custom retrieval logic  
- Less modular system design  

---

## Retriever-Based Retrieval

Retrievers provide a **standard abstraction layer** for retrieving documents.

Instead of directly calling vector database search functions, we convert the vector store into a retriever.

Example:

```python
retriever = vectorstore.as_retriever()

docs = retriever.get_relevant_documents(query)
```

### Workflow

User Question  
↓  
Convert question → embedding  
↓  
Retriever searches vector database  
↓  
Top relevant documents retrieved  
↓  
Documents passed to LLM  

---

## Retriever as an Interface

A retriever acts as an **interface that standardizes retrieval operations**.

Instead of calling different search functions such as:

- `similarity_search()`  
- `mmr_search()`  
- `metadata_filter_search()`  

We simply use:

```python
retriever.get_relevant_documents(query)
```

The retriever internally handles the retrieval logic.

This makes the system **cleaner and easier to integrate with other components**.

---

## Retrieval Strategies

Retrievers support different search strategies.

### 1. Similarity Search

Returns documents whose embeddings are **most similar to the query embedding**.

### 2. Maximum Marginal Relevance (MMR)

Balances **relevance and diversity** in retrieved results.

This avoids retrieving multiple chunks that contain almost identical information.

### 3. Top-K Retrieval

Returns the **top K most relevant documents**.

Example:

```python
retriever = vectorstore.as_retriever(
    search_kwargs={"k":3}
)
```

---

## Analogy (Easy Way to Understand)

Manual Retrieval is like writing a **raw SQL query**:

```sql
SELECT * FROM documents
ORDER BY similarity DESC
LIMIT 3
```

Retriever is like using a **search engine interface**:

```
search_engine.search(query)
```

Both perform retrieval, but the retriever provides a **simplified interface**.

---

## Why Retrievers Are Important in LangChain

Many LangChain components expect a **retriever object**.

Examples:

- RetrievalQA chains  
- Conversational RAG systems  
- Agents with document search  
- Question-answering pipelines  

Example:

```python
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    retriever=retriever
)
```

Because of retrievers, these components can work with **any vector database**.

---

## Key Takeaway

### Manual Retrieval

```python
vectorstore.similarity_search()
```

### Retriever-Based Retrieval

```python
retriever = vectorstore.as_retriever()
retriever.get_relevant_documents()
```

| Manual Retrieval | Retriever |
|------------------|-----------|
| Direct vector database calls | Abstraction layer |
| Harder to integrate | Plug-and-play |
| Less modular | Standard interface |

---

## Final Concept

A **retriever is not a new search algorithm**.

It is an **abstraction/interface that standardizes the process of retrieving relevant documents from vector databases in RAG systems**.