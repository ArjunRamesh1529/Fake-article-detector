# Article Checker

Local RAG fact-checker

## Stack
- **FastAPI + Uvicorn** — backend, auto-launches browser on startup
- **ChromaDB** — persistent vector DB (`./chroma_db`)
- **Ollama** — embeddings (`nomic-embed-text`) + reasoning (`qwen3:8b` or `qwen3:4b`)
- **PyMuPDF** — PDF text extraction
- **python-docx** — DOCX text extraction

## Setup

### 1. Ollama models
```bash
ollama pull nomic-embed-text
ollama pull qwen3:8b    # and/or qwen3:4b
```

### 2. Python environment
```bash
python3 -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Run
```bash
python main.py
```
Browser opens automatically at `http://localhost:8000`.

## Usage

### Fact-check tab (default)
- Paste text **or** upload a `.txt`, `.pdf`, or `.docx` file
- Select model (qwen3:8b / qwen3:4b) and Top-K
- Hit **Check** — results stream in sentence by sentence
- **Left panel**: original text with green (supported) / red (contradicted) highlights
- **Right panel**: verdict, source, matched sentence, and reason per sentence + summary

### Library tab
- Add articles by pasting text or uploading `.txt`, `.pdf`, `.docx`
- Click any article in the list to preview its text in the right panel
- Remove articles with the **Remove** button in the viewer

## Configuration (`main.py` top)

| Variable | Default | Description |
|---|---|---|
| `EMBED_MODEL` | `nomic-embed-text` | Embedding model |
| `DEFAULT_MODEL` | `qwen3:8b` | Default reasoning model |
| `TOP_K` | `8` | Candidates per sentence |
| `CHROMA_PATH` | `./chroma_db` | Vector DB location |
| `PORT` | `8000` | Server port |
