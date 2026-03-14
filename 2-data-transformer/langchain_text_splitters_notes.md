# LangChain Text Splitters

Text Splitters in **LangChain** are used to break large documents into smaller chunks.

Large Language Models (LLMs) have **context limits**, so long documents must be split into smaller pieces before creating embeddings or storing them in vector databases.

Text splitting is an important step in **Retrieval-Augmented Generation (RAG)** systems.

---

# Basic Workflow

```
Raw Document
      ↓
Text Splitter
      ↓
Smaller Text Chunks
      ↓
Embeddings
      ↓
Vector Database
      ↓
Retriever
      ↓
LLM Response
```

---

# Important Parameters

**chunk_size**  
Maximum number of characters allowed in each chunk.

**chunk_overlap**  
Number of characters shared between two consecutive chunks to maintain context.

Example:

```
chunk_size = 100
chunk_overlap = 20
```

```
Chunk 1: characters 0 → 100  
Chunk 2: characters 80 → 180
```

---

# 1. CharacterTextSplitter

`CharacterTextSplitter` splits text using a specified separator such as newline or space.

### Example Text

```
Machine learning is a field of artificial intelligence.
It focuses on building systems that learn from data.
Deep learning is a subset of machine learning.
```

### Example Code

```python
from langchain.text_splitter import CharacterTextSplitter

text_splitter = CharacterTextSplitter(
    separator="\n",
    chunk_size=100,
    chunk_overlap=20
)

chunks = text_splitter.split_text(text)
```

### Example Output

```
Chunk 1:
Machine learning is a field of artificial intelligence.

Chunk 2:
It focuses on building systems that learn from data.

Chunk 3:
Deep learning is a subset of machine learning.
```

---

# 2. RecursiveCharacterTextSplitter

`RecursiveCharacterTextSplitter` is the **most commonly used text splitter**.

It tries multiple separators recursively to split the text in a meaningful way.

### Separator Priority Order

```
["\n\n", "\n", " ", ""]
```

This means it first tries splitting by:

- paragraphs
- lines
- spaces
- characters

### Example Code

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=80,
    chunk_overlap=20
)

chunks = text_splitter.split_text(text)
```

### Example Text

```
Machine learning is a field of artificial intelligence.
It focuses on building systems that learn from data.
Deep learning is a subset of machine learning.
```

### Example Output

```
Chunk 1:
Machine learning is a field of artificial intelligence.

Chunk 2:
It focuses on building systems that learn from data.

Chunk 3:
Deep learning is a subset of machine learning.
```

---

# 3. HTMLHeaderTextSplitter

`HTMLHeaderTextSplitter` is used for splitting **HTML documents based on header tags**.

It keeps the structure of the document intact by grouping content under headers.

### Example HTML

```html
<h1>Introduction</h1>
<p>Machine learning is important.</p>

<h2>Applications</h2>
<p>Used in healthcare and finance.</p>
```

### Example Code

```python
from langchain.text_splitter import HTMLHeaderTextSplitter

headers_to_split_on = [
    ("h1", "Header 1"),
    ("h2", "Header 2"),
]

html_splitter = HTMLHeaderTextSplitter(headers_to_split_on)

documents = html_splitter.split_text(html_content)
```

The output will group content according to the HTML headers.

---

# 4. RecursiveJsonSplitter

`RecursiveJsonSplitter` is used for splitting **structured JSON data**.

It keeps the hierarchical structure of JSON while splitting the content.

### Example JSON

```json
{
  "company": "TechCorp",
  "employees": [
    {"name": "Alice", "role": "Engineer"},
    {"name": "Bob", "role": "Data Scientist"}
  ]
}
```

### Example Code

```python
from langchain.text_splitter import RecursiveJsonSplitter

splitter = RecursiveJsonSplitter(max_chunk_size=200)

chunks = splitter.split_json(json_data)
```

The output will contain smaller JSON chunks while preserving the structure.

---

# Key Idea

Text splitters convert **large documents into manageable chunks**.

These chunks are later used for:

```
Text Splitting
      ↓
Embeddings
      ↓
Vector Database
      ↓
Retriever
      ↓
LLM
```