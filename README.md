<div align="center">
  <img src="https://github.com/user-attachments/assets/0aa67016-6eaf-458a-adb2-6e31a0763ed6" alt="DataNexus AI" width="100%"/>
</div>

# DataNexus AI

[English](README.md) | [中文](README_zh.md)

> 🔮 Transform natural language into powerful SQL queries and stunning visualizations — no SQL expertise required.

DataNexus AI is an intelligent data analysis platform that enables you to interact with databases using plain English. Upload your data files or connect to databases, ask questions in natural language, and get instant SQL queries with beautiful visualizations.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-0.109-green.svg)
![React](https://img.shields.io/badge/React-18.2-61dafb.svg)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.4-38b2ac.svg)

## ✨ Features

### 🤖 AI-Powered SQL Generation
Transform your natural language questions into precise SQL queries. Our AI agent understands your intent and constructs optimized queries automatically.

### 📊 Smart Visualization
Automatic detection of optimal chart types based on your data structure. Line charts, bar charts, pie charts, and more — generated instantly.

### 🗄️ Multi-Source Data Support
- **File Upload**: CSV, Excel (.xlsx), SQLite databases
- **Database Connection**: PostgreSQL, MySQL (via connection string)

### 🧠 Memory-Enabled Conversations
The AI remembers your conversation history, enabling more accurate and context-aware query generation across sessions.

### 📚 Knowledge Base (RAG)
Upload documents to build a custom knowledge base. The AI uses retrieval-augmented generation to answer domain-specific questions.

### 🔒 Secure Authentication
User authentication system with JWT tokens. Your data access is always protected.

## � Screenshots

### 1. Chat History & Main Interface
![Chat History & Query Display](Text2sql/assets/1-chat-history.png)
**Feature: Chat History Management**
- Sidebar displays historical queries in reverse chronological order
- Click any history item to restore the complete conversation and results
- Delete any history record with one click

**Feature: Query Results Display**
- After submission, main interface shows: user question, generated SQL, and result table
- Display loading state like "Thinking..." during processing
- One-click copy for the SQL statement displayed

**Feature: Natural Language Input**
- Submit queries via "Send" button or Enter key
- Input box auto-clears after successful submission
- Empty input prevents submission

---

### 2. Multi-Modal AI Response
![Multi-Modal Response](Text2sql/assets/2-multi-modal-response.png)
The AI agent displays responses with text explanations, SQL code blocks, and query result data simultaneously for comprehensive insights.

---

### 3. Database Connection Configuration
![Database Connection](Text2sql/assets/3-database-connection.png)
**Feature: Database Connection Config**
- Enter database type, address, username, and password to connect and save configuration

**Feature: Connection Test**
- Click "Test Connection" to verify configuration validity
- Immediate success or failure feedback

---

### 4. Long-Term Memory (RAG)
![Long-Term Memory](Text2sql/assets/4-long-term-memory.png)
**Feature: RAG-Based Memory System**
- Save long-term conversation history using RAG for easy retrieval
- Users can rename, delete, or create new memories
- Technologies: memory storage, retrieval, summarization, and injection

---

### 5. Smart Data Visualization
![Data Visualization](Text2sql/assets/5-data-visualization.png)
**Feature: Auto Chart Rendering**
- Frontend automatically renders charts via Recharts library from structured JSON

**Feature: Switch Chart Types**
- Switch to other chart types suggested in the JSON alongside the rendered chart

**Feature: Generate Python Code**
- Select "Generate Code" to display Python code for rendering the current chart

## � Quick Start

### Prerequisites

- Python 3.10+
- Node.js 18+
- Gemini API Key (or OpenAI compatible API)

### 1. Clone the Repository

```bash
git clone https://github.com/sunweihao28/Text2SQL-agent.git
cd Text2SQL-agent/Text2sql
```

### 2. Start the Backend

```bash
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env  # Edit .env with your API keys

# Start the server
uvicorn main:app --reload --port 8000
```

### 3. Start the Frontend

```bash
cd frontend

# Install dependencies
npm install

# Configure environment
cp .env.example .env  # Edit with your API keys

# Start development server
npm run dev
```

### 4. Open the App

Navigate to [http://localhost:5173](http://localhost:5173) in your browser.

## 📖 How to Use

### Step 1: Upload Your Data

Click the **Upload** button in the sidebar to upload:
- 📄 CSV files
- 📊 Excel files (.xlsx)
- 🗃️ SQLite databases

Or connect to an existing PostgreSQL database in Settings.

### Step 2: Ask Questions in Natural Language

Simply type your questions in plain English:

```
"Show me the top 10 customers by revenue last month"
```

```
"Compare sales performance across different regions"
```

```
"What is the average order value for each product category?"
```

### Step 3: Get Instant Results

- **SQL Query**: View the generated SQL with syntax highlighting
- **Execution**: Approve or modify before running
- **Visualization**: Beautiful charts generated automatically
- **Insights**: AI-powered analysis of your results

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Frontend                              │
│                   React + Tailwind CSS                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐ │
│  │  Chat UI    │  │  Settings   │  │  Data Visualization │ │
│  └──────┬──────┘  └──────┬──────┘  └──────────┬──────────┘ │
└─────────┼────────────────┼────────────────────┼────────────┘
          │                │                    │
          └────────────────┼────────────────────┘
                           │ REST API
          ┌────────────────┴────────────────────┐
          │                 Backend              │
          │           FastAPI + SQLAlchemy       │
┌─────────┴─────────┐  ┌──────────┴───────┐  ┌───┴───────────┐
│   Auth Router    │  │   Chat Router    │  │  Upload Router │
└──────────────────┘  └──────────┬───────┘  └────────────────┘
                                 │
                    ┌────────────┴────────────┐
                    │    LLM Service         │
                    │  (Gemini / OpenAI)     │
                    │  + RAG + Memory        │
                    └────────────┬────────────┘
                                 │
          ┌───────────────────────┼───────────────────────┐
          │                       │                       │
┌─────────┴─────────┐  ┌─────────┴─────────┐  ┌─────────┴─────────┐
│   SQLite DB      │  │  File Storage     │  │  Vector DB        │
│  (sql_app.db)    │  │  (uploads/)       │  │  (ChromaDB)       │
└──────────────────┘  └───────────────────┘  └───────────────────┘
```

## 🛠️ Tech Stack

### Backend
- **FastAPI** — High-performance web framework
- **SQLAlchemy** — Database ORM
- **Google Gemini** — Primary LLM
- **OpenAI** — Alternative LLM support
- **LangChain** — LLM framework with RAG
- **ChromaDB** — Vector database for knowledge retrieval
- **Pandas** — Data processing

### Frontend
- **React 18** — UI framework
- **Tailwind CSS** — Styling
- **Recharts** — Data visualization
- **Lucide React** — Icons
- **Vite** — Build tool

## 📁 Project Structure

```
Text2sql/
├── backend/
│   ├── main.py              # FastAPI application entry
│   ├── database.py          # Database configuration
│   ├── models.py            # SQLAlchemy models
│   ├── schemas.py           # Pydantic schemas
│   ├── auth.py              # Authentication
│   ├── routers/
│   │   ├── auth.py          # Auth endpoints
│   │   ├── chat.py          # Chat/SQL endpoints
│   │   ├── upload.py        # File upload endpoints
│   │   ├── rag.py           # RAG endpoints
│   │   └── connection.py     # DB connection endpoints
│   ├── services/
│   │   ├── llm_service.py   # LLM integration
│   │   ├── enhanced_sql.py  # Enhanced SQL generation
│   │   └── rag_service.py   # RAG service
│   ├── utils/
│   │   └── db_utils.py      # Database utilities
│   └── storage/             # File storage
│
└── frontend/
    ├── src/
    │   ├── App.tsx          # Main application
    │   ├── components/      # React components
    │   │   ├── AuthPage.tsx
    │   │   ├── MessageBubble.tsx
    │   │   ├── SettingsModal.tsx
    │   │   └── DataVisualizer.tsx
    │   ├── services/
    │   │   └── api.ts       # API client
    │   └── types.ts         # TypeScript types
    └── package.json
```

## ⚙️ Environment Variables

### Backend (.env)

```env
GEMINI_API_KEY=your_gemini_api_key_here
SECRET_KEY=your_secret_key_here
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=1440
```

### Frontend (.env)

```env
VITE_API_URL=http://localhost:8000/api
```

## 🎯 Use Cases

| Scenario | Example Question |
|----------|------------------|
| Sales Analysis | "What were our best-selling products last quarter?" |
| Customer Insights | "Show customer retention rate by cohort" |
| Financial Reports | "Generate monthly revenue breakdown by region" |
| Inventory | "Which products are below reorder threshold?" |
| Marketing | "What channels drive the highest conversion?" |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

MIT License — see LICENSE file for details.

---

<div align="center">
  <strong>Built with ❤️ by the DataNexus Team</strong>
  <br>
  <a href="https://github.com/sunweihao28/Text2SQL-agent">GitHub</a> · <a href="https://github.com/sunweihao28/Text2SQL-agent/issues">Issues</a>
</div>
