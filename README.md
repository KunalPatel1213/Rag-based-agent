# Full-Stack RAG Application (django + React)

A production-ready Retrieval-Augmented Generation (RAG) system. This project allows users to upload PDF documents, process and embed their contents securely using ChromaDB, and interact with the knowledge base via a streaming, AI-powered chat interface.

The application is built with a decoupled architecture: a blazing-fast **FastAPI backend** handling the AI orchestration and vector database, and a highly responsive **React (Vite) frontend** for the user interface.

## 🌟 Features

* **PDF Ingestion & Processing**: Upload PDFs to break them down into semantically meaningful chunks with intelligent overlap ensuring no context is lost.
* **Vector Search with ChromaDB**: Uses local, persistent ChromaDB to store high-dimensional embeddings for blazing fast and relevant context retrieval.
* **Streaming AI Responses**: Real-time token streaming using Server-Sent Events (SSE) so users aren't waiting for the entire LLM response to generate before reading.
* **Precise Citations**: Automatically tracks document metadata, including file names and page numbers, appending them to generated answers for accuracy and fact-checking.
* **Decoupled Architecture**: Clean separation of concerns between backend logic and UI, making it highly scalable and easy to maintain.
* **Render-Ready**: Includes a complete `render.yaml` Blueprint for 1-click infrastructure-as-code deployment to Render.

## 🛠️ Technology Stack

**Backend**
* [FastAPI](https://fastapi.tiangolo.com/) - High-performance Python web framework
* [LangChain](https://python.langchain.com/) - Orchestration framework for LLMs
* [ChromaDB](https://www.trychroma.com/) - Persistent local vector database
* [OpenRouter](https://openrouter.ai/) - LLM routing and completions (using `gpt-4o-mini` and `text-embedding-3-small`)

**Frontend**
* [React 19](https://react.dev/) - Modern component-based UI
* [Vite](https://vitejs.dev/) - Ultra-fast frontend build tool and dev server

---

## 📂 Project Structure

```text
RAG-CHATBOT/
├── backend/                  # FastAPI Application
│   ├── app/                  # Application source code
│   │   ├── core/             # Configuration & environment setup
│   │   ├── db/               # ChromaDB vector store initialization
│   │   ├── services/         # Core logic: ingestion and RAG streaming
│   │   └── main.py           # API server entrypoint
│   ├── chroma_data/          # Persistent local database directory
│   ├── .env                  # Backend credentials (git-ignored)
│   └── requirements.txt      # Python dependencies
│
├── frontend/                 # React Application (Vite)
│   ├── src/                  # Components, Hooks, API integration
│   ├── package.json          # Node.js dependencies
│   └── vite.config.js        # Vite configuration
│
└── render.yaml               # Infrastructure-as-code deployment config
```

---

## 🚀 Local Development Setup

### 1. Backend Setup

Open a terminal and navigate to the backend directory:
```bash
cd backend
```

Create and activate a virtual environment:
```bash
python -m venv venv
# On Windows:
.\venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate
```

Install dependencies:
```bash
pip install -r requirements.txt
```

Create a `.env` file inside the `backend/` folder and add your credentials:
```env
OPENAI_API_KEY="sk-or-v1-..."  # Your OpenRouter or OpenAI API Key
CHUNK_SIZE=512
CHUNK_OVERLAP=64
```

Start the FastAPI Development Server:
```bash
uvicorn app.main:app --reload --port 8000
```
*The API will be available at [http://localhost:8000](http://localhost:8000)*
*Interactive API docs available at [http://localhost:8000/docs](http://localhost:8000/docs)*

### 2. Frontend Setup

Open a new terminal session and navigate to the frontend directory:
```bash
cd frontend
```

Install Node dependencies:
```bash
npm install
```

Start the Vite Development Server:
```bash
npm run dev
```
*The UI will be available at [http://localhost:5173](http://localhost:5173)*

---

## ☁️ Deployment (Render)

This project features a fully configured `render.yaml` Blueprint which allows you to deploy the frontend and backend simultaneously as Infrastructure-as-code.

1. Push your code to a GitHub/GitLab repository.
2. Log into the [Render Dashboard](https://dashboard.render.com/).
3. Click **New +** and select **Blueprint**.
4. Connect your repository. Render will automatically detect the `render.yaml` file.
5. Provide an `OPENAI_API_KEY` when prompted in the environment variables step.
6. Click **Apply**. 

Render will intelligently deploy a **web service** for your FastAPI backend, and a **Static Site** for your React frontend, securely linking the frontend to the backend's live API URL using `VITE_API_URL` zero-config binding automatically.

## 📝 License

This project is open-source and available under the [MIT License](LICENSE).
