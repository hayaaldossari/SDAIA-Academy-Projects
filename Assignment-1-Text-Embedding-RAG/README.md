# Assignment 1 — Text Embedding and Semantic Search

## Overview

This assignment was developed as part of the **Generative AI Solutions Development** training program.

The project demonstrates a foundational text processing and semantic search pipeline using a text file about **Saudi Projects and Saudi Vision 2030**.

The system processes the document by splitting it into overlapping chunks, counting tokens, generating embeddings, and using cosine similarity to retrieve the most relevant text chunks for a user query. The retrieved context is then provided to a generative AI model to produce a concise answer.

## Objectives

* Load and process a raw `.txt` file.
* Split the text into fixed-size overlapping chunks.
* Count the tokens of each generated chunk.
* Convert text chunks into numerical embeddings.
* Perform semantic similarity search using cosine similarity.
* Retrieve the top 3 most relevant chunks.
* Generate an answer using the retrieved context.

## Dataset

The project uses the following text file:

```text
Saudi Projects & Vision 2030.txt
```

The dataset contains 10 sections covering Saudi projects, organizations, and Vision 2030 programs, including:

* NEOM
* The Line
* Qiddiya
* The Red Sea Project
* Diriyah Gate
* ROSHN
* New Murabba
* Riyadh Metro
* SDAIA
* Quality of Life Program

## Methodology

The pipeline consists of the following steps:

```text
Raw Text
   ↓
Fixed-Size Chunking
   ↓
Tokenization
   ↓
Text Embeddings
   ↓
Cosine Similarity Search
   ↓
Top 3 Relevant Chunks
   ↓
Context + Question
   ↓
Generative AI Answer
```

### 1. Text Chunking

The document is divided into fixed-size character chunks.

The implementation uses:

* Chunk size: **500 characters**
* Overlap: **100 characters**
* Overlap percentage: **20%**

The overlap helps preserve contextual information between neighboring chunks.

### 2. Tokenization

Each generated chunk is passed to the Gemini token counting API to determine its token count.

The project uses:

```text
gemini-3.5-flash-lite
```

for token counting.

### 3. Embeddings

Each text chunk is converted into a numerical vector using:

```text
gemini-embedding-001
```

The same embedding model is also used to convert the user's question into a vector.

### 4. Semantic Similarity Search

The query vector is compared with all stored chunk vectors using **Cosine Similarity**.

The system ranks the chunks according to their similarity scores and retrieves the top 3 most relevant chunks.

### 5. Answer Generation

The retrieved chunks are combined into a context and passed to:

```text
gemini-3.8-flash
```

The model is instructed to answer the question using only the retrieved context.

If the required information cannot be found in the context, the system returns:

```text
I don't have enough information to answer this.
```

## Example Query

```text
What is The Line?
```

The system returns the top 3 relevant chunks together with their cosine similarity scores and then generates an answer based on the retrieved context.

## Technologies Used

* Python
* Google Gemini API
* `google-genai`
* NumPy
* scikit-learn
* Cosine Similarity
* Text Embeddings
* Retrieval-Augmented Generation (RAG)

## Project Structure

```text
Assignment-1-Text-Embedding-RAG/
│
├── Saudi Projects & Vision 2030.txt
├── assignment.py
├── README.md
└── requirements.txt
```

## How to Run

### 1. Install the required libraries

```bash
pip install -r requirements.txt
```

### 2. Add your Gemini API key

Replace the API key placeholder in the Python code with your own Gemini API key.

### 3. Run the Python program

```bash
python assignment.py
```

The program will process the document, generate embeddings, perform semantic search, and generate an answer for the provided question.

## Training Program

This project was developed as part of the:

**Generative AI Solutions Development** training program.

## SDAIA Academy

This project was developed as part of a training program associated with **SDAIA Academy**.

[SDAIA Academy GitHub](https://github.com/SDAIAAcademy)

