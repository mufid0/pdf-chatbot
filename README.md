# 📄 PDF RAG Chatbot

> A conversational AI chatbot that lets users **upload one or more PDF documents and ask questions about their content** using Retrieval-Augmented Generation (RAG).

Built with **LangChain, Google Gemini, FAISS, Sentence Transformers, and Streamlit**.

---

## 🚀 Overview

PDF RAG Chatbot is a document question-answering system that combines **semantic search with Large Language Models (LLMs)**.

Instead of sending an entire PDF to an LLM, the system:

1. Extracts text from uploaded PDFs.
2. Splits the text into smaller, meaningful chunks.
3. Converts chunks into vector embeddings.
4. Stores embeddings in a FAISS vector database.
5. Retrieves the most relevant chunks for a user's question.
6. Passes the retrieved context to Google Gemini.
7. Generates a context-aware answer through a conversational interface.

This approach helps the chatbot answer questions based specifically on the uploaded documents.

---

## ✨ Features

* 📑 **Multiple PDF Support** — Upload and process multiple PDF documents.
* 🔍 **Semantic Search** — Retrieves relevant document sections based on meaning rather than exact keyword matching.
* 🧩 **Intelligent Text Chunking** — Uses LangChain's `RecursiveCharacterTextSplitter`.
* 🧠 **Vector Embeddings** — Generates embeddings using Sentence Transformers.
* ⚡ **FAISS Vector Database** — Enables fast similarity-based document retrieval.
* 💬 **Conversational Chat** — Maintains context across multiple questions.
* 🤖 **Google Gemini Integration** — Uses Gemini through LangChain for answer generation.
* 🖥️ **Streamlit Interface** — Simple web-based interface for document upload and chat.
* ⚙️ **Configurable Pipeline** — Chunk size, overlap, models, and other settings can be configured.
* 🔐 **Environment-Based Configuration** — API keys and sensitive configuration are stored using `.env`.
* 🛡️ **Error Handling** — Includes validation, exception handling, and retry mechanisms.

---

## 🎥 Demo

[▶️ Watch the Demo](https://github.com/user-attachments/assets/a4607370-360f-432a-8dec-4b19ca6e4d99)

The demo shows the complete workflow:

**Upload PDF → Process Documents → Ask Questions → Retrieve Context → Generate Answer**

---

## 🏗️ System Architecture

```text
                ┌─────────────────────┐
                │     PDF Documents   │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │    PDF Extraction   │
                │      PyPDF2         │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │    Text Chunking    │
                │ RecursiveCharacter  │
                │ TextSplitter        │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │     Embeddings      │
                │ SentenceTransformers│
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │   FAISS Vector DB   │
                └──────────┬──────────┘
                           │
                    User Question
                           │
                           ▼
                ┌─────────────────────┐
                │  Similarity Search  │
                │       Top-K         │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Retrieved Context   │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │    Google Gemini    │
                │       LLM           │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │   Final Answer      │
                │   Streamlit UI      │
                └─────────────────────┘
```

---

## 🧠 RAG Pipeline

The application follows a standard Retrieval-Augmented Generation workflow:

### 1. Document Ingestion

Users upload one or more PDF documents through the Streamlit interface.

### 2. Text Extraction

Text is extracted from the PDFs using **PyPDF2**.

### 3. Text Chunking

Large documents are divided into smaller chunks using LangChain's:

```python
RecursiveCharacterTextSplitter
```

Chunk size and overlap can be configured according to the application requirements.

### 4. Embedding Generation

Each text chunk is converted into a numerical vector representation using **Sentence Transformers**.

### 5. Vector Storage

The generated embeddings are stored in a **FAISS vector database**.

### 6. Retrieval

When the user asks a question, the system performs similarity search and retrieves the most relevant document chunks.

### 7. Answer Generation

The retrieved context is passed to **Google Gemini**, which generates the final response.

### 8. Conversational Memory

Previous interactions are maintained using LangChain conversational memory, allowing follow-up questions to be understood in context.

---

## 🛠️ Tech Stack

| Technology                | Purpose                            |
| ------------------------- | ---------------------------------- |
| **Python**                | Core programming language          |
| **LangChain**             | RAG pipeline and LLM orchestration |
| **Google Gemini**         | LLM-based answer generation        |
| **Sentence Transformers** | Text embedding generation          |
| **FAISS**                 | Vector similarity search           |
| **PyPDF2**                | PDF text extraction                |
| **Streamlit**             | Web application interface          |
| **python-dotenv**         | Environment variable management    |

---

## 📂 Project Structure

```text
PDF-RAG-Chatbot/
│
├── app.py
├── requirements.txt
├── .env
├── .gitignore
├── README.md
│
└── src/
    ├── processor.py
    ├── embedding.py
    ├── chat.py
    └── config.py
```

### File Responsibilities

| File               | Description                                           |
| ------------------ | ----------------------------------------------------- |
| `app.py`           | Streamlit interface and application entry point       |
| `processor.py`     | PDF extraction and document chunking                  |
| `embedding.py`     | Embedding generation and FAISS vector store           |
| `chat.py`          | Gemini integration and conversational chat management |
| `config.py`        | Centralized configuration and environment variables   |
| `.env`             | Stores API keys and environment configuration         |
| `requirements.txt` | Python dependencies                                   |

---

## ⚙️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/dksrinath/rag-chatbot.git
cd rag-chatbot
```

### 2. Create a Virtual Environment

**Windows**

```bash
python -m venv venv
venv\Scripts\activate
```

**macOS / Linux**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the project root:

```env
GEMINI_API_KEY=your-gemini-api-key
```

> ⚠️ Never commit your `.env` file or expose your API key publicly.

### 5. Run the Application

```bash
streamlit run app.py
```

The application will start locally and can be accessed through the URL provided by Streamlit.

---

## 💻 Usage

### Step 1 — Upload Documents

Upload one or more PDF files through the sidebar.

### Step 2 — Process Documents

Click **Process Documents**.

The application will:

```text
PDF
 ↓
Text Extraction
 ↓
Chunking
 ↓
Embeddings
 ↓
FAISS Vector Store
```

### Step 3 — Ask Questions

Enter questions related to the uploaded documents.

Example:

```text
What are the main conclusions of the document?
```

or:

```text
Explain the methodology used in this research paper.
```

### Step 4 — Continue the Conversation

Ask follow-up questions without repeating the entire context.

Example:

```text
User: What methodology was used?

User: Why was this methodology selected?

User: What were its limitations?
```

### Step 5 — Clear Conversation

Use **Clear Conversation** to reset the current chat memory.

---

## 🔄 End-to-End Workflow

```text
User
 │
 ▼
Upload PDF(s)
 │
 ▼
Extract Text
 │
 ▼
Split Into Chunks
 │
 ▼
Generate Embeddings
 │
 ▼
Store in FAISS
 │
 ▼
User Question
 │
 ▼
Semantic Similarity Search
 │
 ▼
Retrieve Top-K Chunks
 │
 ▼
Build Context
 │
 ▼
Google Gemini
 │
 ▼
Generate Response
 │
 ▼
Display in Streamlit
```

---

## 🔐 Environment Variables

| Variable         | Description           |
| ---------------- | --------------------- |
| `GEMINI_API_KEY` | Google Gemini API key |

Additional application parameters can be configured through `src/config.py`.

---

## 📌 Key Concepts Demonstrated

This project demonstrates practical implementation of:

* Retrieval-Augmented Generation (RAG)
* Document ingestion pipelines
* PDF text extraction
* Text chunking
* Semantic embeddings
* Vector databases
* FAISS similarity search
* Top-K retrieval
* Prompt construction
* LLM integration
* Conversational memory
* LangChain
* Streamlit application development
* Environment-based configuration

---

## 🚧 Limitations

The current implementation has some limitations:

* Scanned/image-only PDFs may require OCR before text extraction.
* Retrieval quality depends heavily on chunk size, embedding model, and retrieval configuration.
* Very large document collections may require more advanced indexing and storage strategies.
* Conversational memory can increase the amount of context sent to the LLM.
* The system currently relies primarily on semantic retrieval rather than hybrid keyword + vector search.

---

## 🔮 Future Improvements

Potential improvements include:

* [ ] Hybrid search using **BM25 + vector search**
* [ ] Reranking retrieved documents
* [ ] Source citations and page-level references
* [ ] OCR support for scanned PDFs
* [x] Persistent vector database
* [ ] Improved conversational memory
* [ ] Streaming Gemini responses
* [ ] Authentication and user sessions
* [ ] Docker-based deployment
* [ ] Cloud deployment
* [ ] Evaluation using RAG-specific metrics
* [ ] Support for additional document formats

---

## 📈 Possible Evaluation Metrics

For future iterations, the RAG pipeline can be evaluated using metrics such as:

* **Retrieval Precision**
* **Retrieval Recall**
* **Context Relevance**
* **Answer Faithfulness**
* **Answer Relevance**
* **Latency**
* **Token Usage**

This would make the project easier to evaluate beyond simply checking whether the chatbot produces an answer.

---

## 👨‍💻 Author

**Mufid Panhalkar**

Computer Engineering | AI/ML | Generative AI | RAG

* GitHub: [@mufid0](https://github.com/mufid0)
* Portfolio: [mufid0.github.io/Portfolio-Website](https://mufid0.github.io/Portfolio-Website/)

---

## ⭐ If You Find This Project Useful

Consider giving the repository a ⭐ on GitHub.
