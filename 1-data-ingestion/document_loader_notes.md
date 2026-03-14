# LangChain Document Loaders

Document Loaders in **LangChain** are used to load data from different sources and convert it into **LangChain `Document` objects**.

A **Document object** contains:

1. **page_content** → the actual text content  
2. **metadata** → information about the source file  

Example structure:

```python
Document(
    page_content="This is some text",
    metadata={"source": "speech.txt"}
)
```

---

# Why Document Loaders?

LLMs cannot directly read files like **PDF, TXT, XML, etc.**

Document loaders help convert these files into a **standardized format** that LangChain can process.

---

# Basic Workflow

```
File (txt / pdf / xml)
        ↓
Document Loader
        ↓
Document Objects
        ↓
Text Splitting
        ↓
Embeddings
        ↓
Vector Database
```

---

# Common Document Loaders

## 1. TextLoader

Used to load **plain text files**.

### Example

```python
from langchain_community.document_loaders import TextLoader

loader = TextLoader("speech.txt")
documents = loader.load()
```

---

## 2. PyPDFLoader

Used to load **PDF documents**.

### Example

```python
from langchain_community.document_loaders import PyPDFLoader

loader = PyPDFLoader("attention.pdf")
documents = loader.load()
```

---

## 3. XMLLoader

Used to load **XML files**.

### Example

```python
from langchain_community.document_loaders import UnstructuredXMLLoader

loader = UnstructuredXMLLoader("records.xml")
documents = loader.load()
```

LangChain supports **many more document loaders** depending on the data source.

---

# `load()` vs `lazy_load()`

### load()

Loads **all documents at once**.

Useful for **small files**.

### lazy_load()

Loads documents **one by one**.

Useful for **large files or streaming data**.

---

# Key Point

Document loaders convert **raw files into `Document` objects** so that they can be used in the **LangChain pipeline**.

---

