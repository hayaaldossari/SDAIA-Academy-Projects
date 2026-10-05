# Assignment 2 – Phase 2: Retrieval

## Overview

This phase implements the retrieval stage of a Retrieval-Augmented Generation (RAG) system.

The system loads the FAISS vector database and chunk metadata created during Phase 1. It then accepts a user question, converts the question into an embedding using the same embedding model, and searches the vector database for the most relevant chunks.

The retrieved chunks are then provided as context to a language model to generate a concise answer based only on the retrieved information.

## Objectives

The main objectives of this phase are to:

* Load the stored FAISS vector database.
* Load the chunk metadata and file references.
* Convert a user query into an embedding.
* Perform vector similarity search using FAISS.
* Retrieve the top 3 most relevant chunks.
* Display cosine similarity scores and source file names.
* Use the retrieved context to generate an answer.

## Retrieval Pipeline

The retrieval process follows these steps:

```text
User Query
    ↓
Query Embedding
    ↓
FAISS Similarity Search
    ↓
Top-3 Relevant Chunks
    ↓
Context Construction
    ↓
LLM Generation
    ↓
Final Answer
```

## Technologies Used

* Python
* Google Gemini API
* Gemini Embedding Model
* FAISS
* NumPy
* JSON

## Input Files

This phase uses the files generated during Phase 1:

* `places_faiss.index` – FAISS vector database containing the embedded chunks.
* `chunks_metadata.json` – Metadata containing the text chunks and their source file names.

## How It Works

### 1. Load the Vector Database

The previously generated FAISS index is loaded using `faiss.read_index()`.

### 2. Load Chunk Metadata

The metadata file is loaded to associate each retrieved vector with its original text and source file.

### 3. Embed the User Query

The user's question is converted into a numerical vector using the same Gemini embedding model used during Phase 1.

### 4. Similarity Search

The query vector is normalized and searched against the stored vectors in FAISS.

The system retrieves the top 3 most relevant chunks and displays:

* Cosine similarity score
* Source file
* Retrieved text

### 5. Generate the Answer

The retrieved chunks are combined into a context and passed to a Gemini language model.

The model is instructed to answer using only the retrieved context. If the required information is not available, the system returns:

> "I don't have enough information to answer this."

## Example Queries

The system was tested using questions such as:

```text
What is AlUla famous for?
```

and

```text
Which project focuses on entertainment, sports, culture, and tourism?
```

## Output

For each query, the system displays:

```text
QUESTION
↓
TOP RELEVANT CHUNKS
↓
Cosine Similarity Scores
↓
Source File Names
↓
Retrieved Text
↓
ANSWER
```

## Relationship to Phase 1

Phase 1 is responsible for the offline ingestion process:

```text
Text Files
→ Dynamic Chunking
→ Embeddings
→ FAISS Vector Database
→ Chunk Metadata
```

Phase 2 uses these stored outputs without repeating the ingestion process:

```text
User Query
→ Query Embedding
→ FAISS Search
→ Top-K Results
→ LLM Generation
→ Answer
```

## Training Program

This project was developed as part of the **Generative AI Solutions Development** training program by **SDAIA Academy**.

SDAIA Academy GitHub:
https://github.com/SDAIAAcademy

