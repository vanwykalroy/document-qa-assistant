# 📄 Document Q&A Assistant with Knowledge Gap Tracking

An intelligent document assistant that answers questions from any PDF — and automatically logs unanswered queries to Trello so knowledge gaps can be reviewed and addressed.

Built with a RAG (Retrieval-Augmented Generation) pipeline using Meta Llama, semantic search, and Trello systems integration.

---

## What It Does

- Upload any PDF document via Google Drive
- Ask questions in plain English and get answers grounded strictly in the document
- If the document doesn't contain the answer, a Trello card is automatically created for review
- API errors and rate limit failures are handled gracefully — they never create noise tickets

---

## How It Works

The system uses a **Query Fusion RAG pipeline**:

1. Your question is rewritten multiple ways to improve search coverage
2. The document is searched across all query variations
3. The best matching chunks are fused and passed to the AI model
4. The model answers using only what's in the document — no guessing
5. If no answer is found, the query is logged to Trello as a knowledge gap

---

## Tech Stack

| Component | Tool |
|---|---|
| AI Model | Meta Llama 3.3 70B via OpenRouter |
| RAG Framework | LlamaIndex |
| Embeddings | BAAI/bge-small-en-v1.5 (HuggingFace) |
| Chunking | Semantic Splitter (LlamaIndex) |
| Retrieval | Query Fusion / Query Rewriting |
| Systems Integration | Trello REST API |
| Runtime | Google Colab |

---

## Prerequisites

Before running the notebook, make sure you have:

- A free [OpenRouter account](https://openrouter.ai) and API key
- A [Trello account](https://trello.com) with an API key and Token
- A Trello board named **"Document Assistant — Knowledge Gaps"** with a list named **"Unanswered Queries"**
- A PDF stored in Google Drive (set to *Anyone with the link can view*)

---

## Setup & Usage

### 1. Open in Google Colab
Upload the `.ipynb` file to [Google Colab](https://colab.research.google.com) or open it directly from this repo.

### 2. Run the cells in order

| Step | What it does |
|---|---|
| Step 1 | Installs all required libraries |
| Step 2 | Connects to Meta Llama via OpenRouter |
| Step 3 | Connects to your Trello board |
| Step 4 | Downloads your PDF from Google Drive |
| Step 5 | Splits the document into semantic chunks |
| Step 6 | Builds the Query Fusion retrieval engine |
| Step 7 | Starts the interactive Q&A session |

### 3. Ask questions
Type any question about your document. Type `exit` to end the session.

---

## Trello Integration

When a question cannot be answered from the document, a card is automatically created in the **"Unanswered Queries"** list with:

- The user's question
- The document name
- Timestamp
- Number of chunks retrieved (if any)

**What does NOT create a ticket:**
- OpenRouter API rate limit errors
- Network timeouts or connection failures
- Any infrastructure-level exception

This keeps the Trello board clean and meaningful — only genuine knowledge gaps are logged.

---

## Example Questions to Try

- *"What are the main goals described in this document?"*
- *"What does this policy say about deadlines?"*
- *"Summarise the key points from section two."*
- *"What responsibilities are listed for staff members?"*

---

## Notes

- The free tier of OpenRouter may occasionally hit rate limits. If this happens, wait a moment and retry — no Trello ticket will be created.
- For best results, use PDFs with clear, readable text (not scanned images).
- The semantic chunker works best on documents longer than 5 pages.
