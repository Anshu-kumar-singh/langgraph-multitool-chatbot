# 🚀 Multi-Utility AI Chatbot with LangGraph, RAG & Streamlit

A production-style **AI chatbot** built using **LangGraph**, **LangChain**, and **Streamlit** that combines **Retrieval-Augmented Generation (RAG)** with multiple intelligent tools.

Unlike a traditional chatbot, this application can:

* 📄 Answer questions from uploaded PDF documents
* 🌐 Search the web when external information is needed
* 📈 Fetch live stock prices
* 🧮 Perform mathematical calculations
* 💾 Maintain persistent multi-thread conversations
* ⚡ Automatically decide when to use tools through LangGraph's tool-calling workflow

---

# 📸 Demo

> Add screenshots or a GIF here

```
/images
    ├── home.png
    ├── pdf-upload.png
    ├── tool-calling.png
    └── chat-history.png
```

---

# ✨ Features

## 📄 PDF Question Answering (RAG)

* Upload any PDF document.
* Automatically extracts text.
* Splits documents into optimized chunks.
* Generates vector embeddings.
* Stores embeddings inside a FAISS vector database.
* Retrieves the most relevant chunks for every question.

---

## 🤖 Intelligent Tool Calling

The LLM automatically decides whether it should answer directly or invoke one of the available tools.

### Available Tools

* 🔍 DuckDuckGo Web Search
* 📈 Live Stock Price Lookup (Alpha Vantage API)
* 🧮 Calculator
* 📄 PDF Retrieval Tool (RAG)

No manual routing is required.

---

## 💬 Persistent Conversations

Each chat session receives its own unique Thread ID.

Conversation history is stored using:

* LangGraph Checkpointer
* SQLite Database

This allows:

* Resume previous conversations
* Switch between chats
* Maintain context across sessions

---

## 📚 Thread-Specific Document Memory

Every conversation maintains its own independent document index.

Example:

Thread A

```
Machine Learning.pdf
```

Thread B

```
Finance Report.pdf
```

Questions in Thread A will never retrieve content from Thread B.

---

## ⚡ Streaming Responses

Responses are streamed token-by-token for a smooth ChatGPT-like experience.

Tool execution is also displayed live through Streamlit status indicators.

---

## 🎯 Modern Streamlit Interface

The UI includes:

* PDF uploader
* Chat interface
* Conversation history
* New Chat button
* Thread switching
* Document status
* Tool execution status

---

# 🏗️ Architecture

```
                User
                  │
                  ▼
          Streamlit Frontend
                  │
                  ▼
            LangGraph Graph
                  │
      ┌───────────┴────────────┐
      │                        │
      ▼                        ▼
   Chat Node              Tool Node
      │                        │
      │                ┌───────────────┐
      │                │ DuckDuckGo    │
      │                │ Calculator    │
      │                │ Stock API     │
      │                │ PDF Retriever │
      │                └───────────────┘
      │
      ▼
      LLM
      │
      ▼
 Streamed Response
```

---

# 🛠️ Tech Stack

## Frontend

* Streamlit

## LLM

* Groq
* Llama 3.3 70B Versatile

## Frameworks

* LangChain
* LangGraph

## Vector Database

* FAISS

## Embeddings

* sentence-transformers/all-MiniLM-L6-v2

## PDF Processing

* PyPDF
* RecursiveCharacterTextSplitter

## Database

* SQLite

---

# 📂 Project Structure

```
project/
│
├── streamlit_rag_frontend.py
├── langraph_rag_backend.py
├── requirements.txt
├── chatbot.db
├── .env
└── README.md
```

---

# ⚙️ Installation

## 1. Clone the repository

```bash
git clone https://github.com/your-username/your-repository.git

cd your-repository
```

---

## 2. Create a virtual environment

Windows

```bash
python -m venv venv

venv\Scripts\activate
```

Linux / macOS

```bash
python3 -m venv venv

source venv/bin/activate
```

---

## 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 4. Create a `.env` file

```env
GROQ_API_KEY=your_groq_api_key
```

---

## 5. Run the application

```bash
streamlit run streamlit_rag_frontend.py
```

---

# 📖 How It Works

## Step 1

User uploads a PDF.

↓

## Step 2

The backend

* loads the PDF
* splits it into chunks
* generates embeddings
* stores them in FAISS

↓

## Step 3

User asks a question.

↓

## Step 4

LangGraph sends the conversation to the LLM.

↓

## Step 5

The LLM decides whether to:

* answer directly
* search the web
* retrieve from PDF
* perform calculations
* fetch stock prices

↓

## Step 6

Tool results are returned to the LLM.

↓

## Step 7

The final answer is streamed back to the UI.

---

# 🧠 LangGraph Workflow

```
                START
                   │
                   ▼
             Chat Node (LLM)
                   │
         Tool Needed?
          │             │
          │No           │Yes
          ▼             ▼
        Finish      Tool Node
                         │
                         ▼
                  Execute Tool
                         │
                         ▼
                    Chat Node
                         │
                         ▼
                       END
```

---

# 🔧 Implemented Tools

## 📄 RAG Tool

Retrieves relevant chunks from the uploaded PDF using semantic similarity search.

---

## 🔍 Web Search Tool

Uses DuckDuckGo Search for retrieving external information.

---

## 📈 Stock Price Tool

Fetches the latest stock information using the Alpha Vantage API.

---

## 🧮 Calculator Tool

Supports:

* Addition
* Subtraction
* Multiplication
* Division

---

# 💾 Conversation Persistence

The application uses SQLite through LangGraph's checkpointer to persist:

* Chat history
* Thread IDs
* Conversation state

Each chat behaves independently, enabling multiple ongoing conversations without losing context.

---

# 🚀 Future Improvements

* User authentication
* Multiple document retrieval
* Hybrid Search (BM25 + Vector Search)
* Source citations
* Conversation export
* Cloud deployment
* PostgreSQL support
* Docker support
* OCR for scanned PDFs
* Image understanding
* Voice input/output
* Multi-agent workflows

---

# 📋 Requirements

Core dependencies include:

```
streamlit
langgraph
langchain
langchain-community
langchain-groq
langchain-huggingface
faiss-cpu
sentence-transformers
pypdf
python-dotenv
requests
ddgs
```

---

# 🤝 Contributing

Contributions are welcome!

If you'd like to improve the project:

1. Fork the repository.
2. Create a feature branch.
3. Commit your changes.
4. Push the branch.
5. Open a Pull Request.

---

# 📄 License

This project is licensed under the MIT License.

---

# ⭐ Acknowledgements

Built using:

* LangGraph
* LangChain
* Streamlit
* FAISS
* Hugging Face Sentence Transformers
* Groq
* DuckDuckGo Search
* Alpha Vantage API

---

## 👨‍💻 Author

Developed as a practical demonstration of building a production-inspired **Retrieval-Augmented Generation (RAG)** chatbot with **LangGraph**, integrating document retrieval, tool calling, persistent conversation memory, and a modern Streamlit interface.
