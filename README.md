# Gemini File Search API Demo (RAG with Metadata)

This Jupyter Notebook demonstrates how to build a Retrieval-Augmented Generation (RAG) pipeline using the **Google GenAI SDK** (`google-genai`). 

It automates the process of creating a vector store, uploading documents with custom metadata, performing a query with citations, and cleaning up resources afterward.

## 🚀 Features

* [cite_start]**Automated Ingestion**: Scans a local folder (`my_docs`) and uploads supported files (PDF, TXT, JSON, MD, CSV) to a Gemini File Search Store[cite: 12].
* [cite_start]**Smart Metadata Tagging**: Automatically assigns categories (`finance`, `technical`, `general`) based on filenames during upload[cite: 10, 11].
* [cite_start]**RAG Querying**: Uses the `gemini-2.5-flash` model to answer questions based *only* on the uploaded documents[cite: 9, 42].
* [cite_start]**Citation Parsing**: Includes a utility function to parse and display exact source citations and grounding chunks from the model's response[cite: 24, 28].
* [cite_start]**Resource Cleanup**: Includes a "force delete" function to ensure the File Store is completely removed after use to save costs/storage[cite: 21, 22].

## 🛠️ Prerequisites

* Python 3.12+ (Recommended)
* A Google Cloud Project with the Gemini API enabled.
* An API Key from Google AI Studio.

## 📦 Installation

Install the Google GenAI SDK:

```bash
pip install google-genai
