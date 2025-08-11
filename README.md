# RAG Q&A for YouTube Videos

A lightweight Notebook that turns a YouTube video transcript into a retrievable knowledge base.  
Provide a YouTube **video ID** (or URL if you parse the ID), then ask questions — the notebook fetches transcripts, creates embeddings, stores vectors in FAISS, and answers using LangChain + OpenAI.

## Features
- Fetches captions with `youtube-transcript-api`
- Splits transcript into chunks (`RecursiveCharacterTextSplitter`)
- Creates embeddings via OpenAI (`text-embedding-3-small`)
- Stores vectors in FAISS for fast semantic search
- Uses LangChain `PromptTemplate` + `ChatOpenAI` to answer user questions based only on retrieved context

## Requirements
- Python 3.9+
- Set `OPENAI_API_KEY` in environment (or use `.env`)
- Key packages (from notebook):
  - `youtube-transcript-api`
  - `langchain-community`, `langchain-openai`, `langchain-core`
  - `faiss-cpu`
  - `tiktoken`, `python-dotenv`

Install example (from notebook):
```bash
pip install youtube-transcript-api langchain-community langchain-openai \
            faiss-cpu tiktoken python-dotenv


flowchart LR
  A[YouTube URL / Video ID] --> B[Transcript Fetcher]
  B --> C[Text Splitter (chunks)]
  C --> D[Embedding Model (OpenAI)]
  D --> E[Vector Store (FAISS)]
  E --> F[Retriever (semantic search)]
  F --> G[Prompt Builder (context + question)]
  G --> H[LLM (ChatOpenAI)]
  H --> I[Response to User]

