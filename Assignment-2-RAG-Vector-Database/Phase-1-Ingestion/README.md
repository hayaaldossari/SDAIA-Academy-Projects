# Phase 1 — Ingestion

## Overview

This phase implements the **Ingestion Phase** of a Retrieval-Augmented Generation (RAG) pipeline.

The system loads three text documents related to **Saudi Arabia, tourism, heritage, culture, and Vision 2030**, processes the documents using dynamic text chunking, converts each chunk into a numerical embedding, and stores the embeddings in a **FAISS vector database**.

The generated metadata is also saved to maintain the relationship between each chunk and its original source file.

## Objectives

* Load multiple `.txt` files into Python.
* Apply dynamic text chunking.
* Preserve the source file for each generated chunk.
* Count the tokens of each chunk.
* Generate embeddings for all chunks.
* Normalize the embedding vectors.
* Create a FAISS vector index using cosine similarity.
* Save the vector database for use in Phase 2.
* Save chunk metadata for retrieval and source referencing.

## Input Documents

The ingestion pipeline processes three text files:

```text
Saudi Projects & Vision 2030.txt
Saudi Tourism.txt
Saudi heritage and culture.txt
```

The documents contain information related to Saudi projects, tourism, heritage, culture, and Vision 2030.

## Ingestion Pipeline

```text
Text Files
    ↓
Load Documents
    ↓
Dynamic Text Chunking
    ↓
Token Counting
    ↓
Text Embeddings
    ↓
Vector Normalization
    ↓
FAISS Vector Database
    ↓
Save Metadata
```

## 1. Document Loading

The program reads the three `.txt` files using UTF-8 encoding.

For every document, the system stores:

* The file name
* The document text

The number of characters in each document is also displayed.

## 2. Dynamic Text Chunking

The documents are divided into chunks using a dynamic chunking approach.

The chunking process:

1. Splits the document into paragraphs.
2. Splits paragraphs into sentences.
3. Combines sentences until the chunk reaches the maximum character limit.
4. Creates a new chunk when the limit is exceeded.

The maximum chunk size is:

```text
700 characters
```

Unlike fixed-size chunking, this approach uses sentence boundaries when constructing the chunks.

## 3. Source References

Each generated chunk is stored together with its original file name.

Each chunk follows this structure:

```python
{
    "text": chunk,
    "file_name": file_name
}
```

This allows the system to identify the source document of each retrieved chunk during the retrieval phase.

## 4. Token Counting

The token count of every generated chunk is calculated using the Gemini API.

The model used for token counting is:

```text
gemini-3.8-flash
```

The token count for each chunk is printed during execution.

## 5. Text Embeddings

Each chunk is converted into a numerical vector using:

```text
gemini-embedding-2
```

The resulting vectors are stored in an embeddings list and then converted into a NumPy matrix.

The embedding matrix is stored as:

```text
float32
```

## 6. FAISS Vector Database

The embedding vectors are normalized before being added to FAISS.

```python
faiss.normalize_L2(embedding_matrix)
```

A FAISS `IndexFlatIP` index is then created.

Because the vectors are normalized, inner product can be used to perform cosine similarity search.

The generated vector database is saved as:

```text
places_faiss.index
```

## 7. Chunk Metadata

The chunk information is saved separately as JSON.

The metadata file contains the generated chunks and their corresponding source file names.

The file is:

```text
chunks_metadata.json
```

This metadata is used in Phase 2 to identify the source of retrieved chunks.

## Output Files

After running the ingestion notebook, the following files are generated:

```text
places_faiss.index
chunks_metadata.json
```

These files are required by the retrieval phase.

## Technologies Used

* Python
* Google Gemini API
* `google-genai`
* FAISS
* NumPy
* JSON
* Regular Expressions

## Project Structure

```text
Phase-1-Ingestion/
│
├── Phase_1_Ingestion.ipynb
├── Saudi Projects & Vision 2030.txt
├── Saudi Tourism.txt
├── Saudi heritage and culture.txt
├── places_faiss.index
├── chunks_metadata.json
├── README.md
└── requirements.txt
```

## Requirements

The required Python packages are listed in:

```text
requirements.txt
```

Install them using:

```bash
pip install -r requirements.txt
```

## API Key

The project uses the Google Gemini API.

Before running the notebook, provide a valid Gemini API key in the client configuration:

```python
client = genai.Client(api_key="API_KEY_HERE")
```

For security, API keys should not be committed or uploaded to GitHub.

## Training Program

This project was developed as part of the **Generative AI Solutions Development** training program associated with **SDAIA Academy**.

[SDAIA Academy GitHub](https://github.com/SDAIAAcademy)

