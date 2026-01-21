# Gemini File Search API Demo (RAG with Metadata)

This Jupyter Notebook demonstrates how to build a Retrieval-Augmented Generation (RAG) pipeline using the **Google GenAI SDK** (`google-genai`).

It automates the process of creating a vector store, uploading documents with custom metadata, performing queries with citations, and cleaning up resources afterward.

## 🚀 Features

- **Automated Document Generation**: Creates dummy legal documents (JSON format) with realistic case data including titles, case IDs, dates, parties, and summaries.
- **File Search Store Management**: Creates and manages Gemini File Search Stores for document indexing.
- **Smart Metadata Tagging**: Assigns custom metadata (`status`, `uploaded_via`, `category`) to documents during upload.
- **RAG Querying**: Uses the `gemini-2.5-flash` model to answer questions based on the uploaded documents with metadata filtering.
- **Citation Parsing**: Includes a utility function to parse and display exact source citations and grounding chunks from the model's response.
- **Resource Cleanup**: Includes a "force delete" function to ensure the File Store is completely removed after use to save costs/storage.

## 🛠️ Prerequisites

- Python 3.12+ (Recommended)
- A Google Cloud Project with the Gemini API enabled
- An API Key from [Google AI Studio](https://aistudio.google.com/)

## 📦 Installation

Install the Google GenAI SDK:

```bash
pip install google-genai
```

## 📁 Project Structure

```
gemini-file-search/
├── Gemini_File_Search_Notebook_Demo.ipynb  # Main demo notebook
├── README.md                                # This file
├── LICENSE                                  # MIT License
├── .gitignore                               # Python gitignore
└── my_docs/                                 # Generated at runtime (dummy legal documents)
```

## 🚀 Usage

1. **Clone the repository**:
   ```bash
   git clone https://github.com/cloudbloqavi/gemini-file-search.git
   cd gemini-file-search
   ```

2. **Set up your API key**:
   Replace the placeholder in the notebook with your actual Gemini API key:
   ```python
   os.environ["GEMINI_API_KEY"] = "your-api-key-here"
   ```

3. **Run the notebook**:
   Open [`Gemini_File_Search_Notebook_Demo.ipynb`](Gemini_File_Search_Notebook_Demo.ipynb) in Jupyter Notebook, Google Colab, or VS Code and execute the cells in order.

## 📝 Notebook Workflow

The notebook follows this workflow:

1. **Generate Dummy Documents**: Creates 10 legal document JSON files with randomized case data in the `my_docs/` folder.

2. **Initialize Client**: Sets up the Google GenAI client with your API key.

3. **Create File Search Store**: Creates a new vector store for document indexing.

4. **Upload Documents with Metadata**: 
   - Scans the `my_docs/` folder for supported files (`.txt`, `.pdf`, `.csv`, `.md`, `.json`)
   - Uploads each file with custom metadata
   - Returns document IDs for database reference

5. **Query with RAG**: 
   - Asks questions against the uploaded documents
   - Uses metadata filtering (`status=active`)
   - Returns grounded answers with source citations

6. **Cleanup**: Force deletes the File Search Store and all contained documents.

## 🔍 Example Query

```python
question = "What happened to Plaintiff_76? Give me a brief summary."

response = client.models.generate_content(
    model=MODEL_ID,
    contents=question,
    config=types.GenerateContentConfig(
        tools=[
            types.Tool(
                file_search=types.FileSearch(
                    file_search_store_names=[store.name],
                    metadata_filter="status=active",
                )
            )
        ]
    )
)
```

## 📊 Citation Output Example

The notebook parses and displays citations in a readable format:

```
==================== CITATIONS ====================
📝 CLAIM: "...Plaintiff_76 was involved in a dispute over..."
   ↳ SOURCE: legal_document_3.json
----------------------------------------
```

## ⚙️ Configuration

Key configuration variables in the notebook:

| Variable | Description | Default |
|----------|-------------|---------|
| `API_KEY` | Your Gemini API key | From environment |
| `FOLDER_PATH` | Path to documents folder | `my_docs` |
| `STORE_NAME` | Display name for the store | `rooms_reference_store` |
| `MODEL_ID` | Gemini model to use | `gemini-2.5-flash` |

## 🗂️ Supported File Types

The notebook supports the following file formats for upload:
- `.txt` - Plain text files
- `.pdf` - PDF documents
- `.csv` - CSV data files
- `.md` - Markdown files
- `.json` - JSON documents

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Open issues for bugs or feature requests
- Submit pull requests with improvements
- Share feedback and suggestions

## 🔗 Resources

- [Google GenAI SDK Documentation](https://ai.google.dev/gemini-api/docs)
- [Gemini API File Search Documentation](https://ai.google.dev/gemini-api/docs/file-search)
- [Google AI Studio](https://aistudio.google.com/)

---

Made with ❤️ by [cloudbloqavi](https://github.com/cloudbloqavi)
