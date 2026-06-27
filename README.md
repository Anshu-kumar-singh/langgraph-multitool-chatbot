# 🚀 Multi-Utility AI Chatbot with LangGraph, RAG & Streamlit

A production-style **AI chatbot** built using **LangGraph**, **LangChain**, and **Streamlit** that combines **Retrieval-Augmented Generation (RAG)** with multiple intelligent tools.

🚀 **Live Demo:** https://anshu908-chat-bot.hf.space

Unlike a traditional chatbot, this application can:

* 📄 Answer questions from uploaded PDF documents
* 🌐 Search the web when external information is needed
* 📈 Fetch live stock prices
* 🧮 Perform mathematical calculations
* 💾 Maintain persistent multi-thread conversations
* ⚡ Automatically decide when to use tools through LangGraph's tool-calling workflow

---

# 🚀 Live Demo

🌐 **Try the application here:**

**https://anshu908-chat-bot.hf.space**

No installation required—simply open the application, upload a PDF (optional), and start chatting.

---

# 📸 Demo

> Add screenshots or a GIF here

```text
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

This allows users to:

* Resume previous conversations
* Switch between chats
* Maintain context across sessions

---

## 📚 Thread-Specific Document Memory

Every conversation maintains its own independent document index.

Example:

**Thread A**

```text
Machine Learning.pdf
```

**Thread B**

```text
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

```text
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

```text
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

## 1. Clone the Repository

```bash
git clone https://github.com/your-username/your-repository.git

cd your-repository
```

---

## 2. Create a Virtual Environment

### Windows

```bash
python -m venv venv

venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv venv

source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 4. Create a `.env` File

```env
GROQ_API_KEY=your_groq_api_key
```

---

# ▶️ Running the Application

## Option 1: Use the Live Demo

Open your browser and visit:

**https://anshu908-chat-bot.hf.space**

---

## Option 2: Run Locally

```bash
streamlit run streamlit_rag_frontend.py
```

The application will launch on your local Streamlit server.

---

# 📖 How It Works

### Step 1

The user uploads a PDF (optional).

↓

### Step 2

The backend:

* Loads the PDF
* Splits it into semantic chunks
* Generates embeddings
* Stores them inside a FAISS vector database

↓

### Step 3

The user submits a question.

↓

### Step 4

LangGraph sends the conversation to the LLM.

↓

### Step 5

The LLM automatically decides whether to:

* Answer directly
* Search the web
* Retrieve information from the uploaded PDF
* Perform mathematical calculations
* Fetch live stock prices

↓

### Step 6

The selected tool executes and returns its result.

↓

### Step 7

The LLM synthesizes the final response and streams it back to the Streamlit interface.

---

# 🧠 LangGraph Workflow

```text
                START
                   │
                   ▼
             Chat Node (LLM)
                   │
          Tool Needed?
           │           │
        No │           │ Yes
           ▼           ▼
       Final      Execute Tool
      Response         │
                       ▼
                  Tool Result
                       │
                       ▼
                 Chat Node (LLM)
                       │
                       ▼
                      END
```

---

# 🔧 Implemented Tools

## 📄 PDF Retrieval Tool (RAG)

Retrieves the most relevant document chunks using semantic similarity search over FAISS.

---

## 🔍 DuckDuckGo Web Search

Retrieves external information when knowledge is unavailable in the uploaded documents.

---

## 📈 Stock Price Tool

Fetches live stock prices using the Alpha Vantage API.

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

Each conversation behaves independently, enabling multiple ongoing chats without losing context.

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

```text
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

MIT License

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

# 👨‍💻 Author

Developed as a production-style AI chatbot demonstrating **LangGraph**, **Retrieval-Augmented Generation (RAG)**, intelligent tool calling, persistent conversation memory, and a modern Streamlit interface. The project showcases how a single conversational AI system can seamlessly combine document understanding, web search, live stock data retrieval, mathematical reasoning, and multi-thread chat persistence within an extensible agentic workflow.
