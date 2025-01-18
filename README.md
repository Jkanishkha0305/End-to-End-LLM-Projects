# End-to-End LLM Projects

<p align="center">
  <img src="https://img.shields.io/badge/LangChain-Projects-blue?style=flat-square" />
  <img src="https://img.shields.io/badge/RAG-Pipelines-blueviolet?style=flat-square" />
  <img src="https://img.shields.io/badge/OpenAI-412991?logo=openai&style=flat-square" />
  <img src="https://img.shields.io/badge/Groq-Fast%20Inference-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Streamlit-FF4B4B?logo=streamlit&style=flat-square" />
  <img src="https://img.shields.io/badge/Python-3.11-3776AB?logo=python&style=flat-square" />
</p>

> **Collection of production-ready LLM projects** — each project is fully self-contained with RAG pipelines, tool-calling agents, document Q&A systems, and more.

## Projects

| Project | Description | Stack |
|---------|-------------|-------|
| `pdf-chat/` | Chat with any PDF document | LangChain, FAISS, GPT-4 |
| `sql-agent/` | Natural language → SQL queries | LangChain, SQLite, GPT-4 |
| `web-researcher/` | Autonomous web research agent | LangChain, Tavily, GPT-4 |
| `code-reviewer/` | Automated code review pipeline | LangChain, GitHub API |
| `multi-doc-rag/` | RAG over multiple document types | Chroma, OpenAI Embeddings |
| `summarizer/` | Long document summarization | Map-reduce chain, Groq |

## Quick Start

```bash
git clone https://github.com/Jkanishkha0305/End-to-End-LLM-Projects.git
cd End-to-End-LLM-Projects

# Run any project
cd pdf-chat
pip install -r requirements.txt
cp .env.example .env  # add OPENAI_API_KEY
streamlit run app.py
```

## Tech Stack

- **LangChain** — chains, agents, and tool use
- **OpenAI / Groq** — LLM providers
- **FAISS / Chroma** — vector stores
- **Streamlit / Gradio** — demo frontends
