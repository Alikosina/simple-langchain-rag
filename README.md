# Restaurant RAG

A RAG system for restaurant recommendations: answers questions about a venue using reviews from a dataset, not only the model's prior knowledge.

The user asks a question in the terminal → the system retrieves relevant reviews → the LLM generates an answer based on them.

## Stack

| Component | Technology |
|-----------|------------|
| Orchestration | LangChain |
| LLM | Ollama (`llama3.2`) |
| Embeddings | Ollama (`mxbai-embed-large`) |
| Vector store | Chroma |
| Data | Pandas + CSV reviews |
| Monitoring | LangFuse |

Also uses `python-dotenv` for configuration and the LangFuse CallbackHandler to trace prompts and model responses.

## How it works

1. `vector.py` loads reviews from `realistic_restaurant_reviews.csv`, builds embeddings, and stores them in Chroma.
2. `main.py` takes a question, retrieves the top-k relevant reviews via the retriever, and passes them into the prompt with the question.
3. Ollama generates the answer; LangFuse records the calls for monitoring and debugging.

## Getting started

1. Copy `.env.example` to `.env` and fill in the keys (Ollama host, LangFuse).
2. Install dependencies:

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

3. Make sure Ollama is running and the `llama3.2` and `mxbai-embed-large` models are available.
4. Run the app:

```bash
python main.py
```

Enter a question, or `q` to quit.
