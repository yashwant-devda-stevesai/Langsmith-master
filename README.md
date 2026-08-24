# LangSmith Masterclass

A collection of small, runnable examples for learning LangChain, LangSmith tracing, retrieval-augmented generation (RAG), tool-using agents, and LangGraph workflows.

## Examples

| File | Topic |
| --- | --- |
| `1_simple_llm_call.py` | A basic prompt -> OpenAI chat model -> string parser chain |
| `2_sequential_chain.py` | A sequential chain that generates a report and then summarizes it |
| `3_rag_v1.py` | PDF RAG with chunking, OpenAI embeddings, and a FAISS vector store |
| `3_rag_v2.py` | Adds LangSmith tracing around PDF loading, splitting, indexing, and querying |
| `3_rag_v3.py` | Groups setup and query work under a traced parent run |
| `3_rag_v4.py` | Caches FAISS indexes using a PDF and configuration fingerprint |
| `4_agent.py` | ReAct agent with DuckDuckGo search and a weather tool |
| `5_langgraph.py` | Parallel essay evaluation with structured output and LangGraph |

The RAG examples use [`islr.pdf`](islr.pdf) as their sample source document.

## Requirements

- Python 3.10 or newer
- An OpenAI API key
- A LangSmith API key for the tracing examples
- A Weatherstack API key for the weather tool in `4_agent.py`

## Setup

Create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install the dependencies:

```powershell
python -m pip install -r requirements.txt
```

Create a `.env` file in the project root:

```dotenv
OPENAI_API_KEY=your-openai-api-key
LANGCHAIN_TRACING_V2=true
LANGCHAIN_API_KEY=your-langsmith-api-key
LANGCHAIN_PROJECT=langsmith-masterclass
```

`LANGCHAIN_TRACING_V2`, `LANGCHAIN_API_KEY`, and `LANGCHAIN_PROJECT` are optional for examples that do not use LangSmith tracing. Set `LANGCHAIN_ENDPOINT` as well if your LangSmith deployment requires a custom endpoint.

## Run an example

Run scripts from the project root so that relative paths such as `islr.pdf` resolve correctly:

```powershell
python 1_simple_llm_call.py
python 2_sequential_chain.py
python 3_rag_v1.py
python 3_rag_v2.py
python 3_rag_v3.py
python 3_rag_v4.py
python 4_agent.py
python 5_langgraph.py
```

The RAG examples prompt for a question in the terminal. The first run of `3_rag_v4.py` builds a FAISS index in `.indices`; later runs reuse it unless the PDF or index configuration changes.

## LangSmith tracing

When tracing is enabled, runs appear in the LangSmith project configured by `LANGCHAIN_PROJECT`. The later examples demonstrate traced helper functions, parent runs, tags, metadata, and LangGraph node execution.

## Notes

- `3_rag_v1.py` through `3_rag_v4.py` expect `islr.pdf` in the project root. Change `PDF_PATH` to use another PDF.
- The RAG examples send document content to OpenAI for embeddings and answer generation.
- `4_agent.py` currently contains a Weatherstack credential in source code. Replace it with an environment variable and rotate the exposed credential before publishing or deploying this project.
- `.indices` contains generated local FAISS data and can be deleted to rebuild the cache.

## License

No license file is currently included in this repository.
