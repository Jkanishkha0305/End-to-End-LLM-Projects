# Project Index — End-to-End-LLM-Projects

Complete guide to all LLM projects in this repository.

## Projects

| # | Project | Use Case | Model | Stack | Notebook |
|---|---------|----------|-------|-------|---------|
| 1 | RAG Pipeline | Document Q&A | GPT-4 / Llama | LangChain, FAISS, FastAPI | `01-rag-pipeline/` |
| 2 | Text Summarization | Long-form summarization | BART / T5 | HuggingFace, Gradio | `02-text-summarizer/` |
| 3 | Code Generation | Code assistant | CodeLlama | LangChain, Streamlit | `03-code-gen/` |
| 4 | Sentiment Analysis | Financial NLP | FinBERT | Transformers, Flask | `04-sentiment/` |
| 5 | Chatbot | Conversational AI | GPT-3.5 | LangChain, memory | `05-chatbot/` |
| 6 | Image Captioning | Vision-language | BLIP-2 | Transformers, Gradio | `06-image-caption/` |

## How to Run Any Project

```bash
cd <project-folder>/
pip install -r requirements.txt
# Set API keys in .env
python app.py  # or: jupyter notebook
```

## Common Dependencies

- `langchain`, `langchain-community`
- `openai`, `huggingface-hub`, `transformers`
- `fastapi`, `streamlit`, `gradio`
- `faiss-cpu`, `chromadb`
