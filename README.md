LLM Book Recommender
A semantic book recommender that matches a user’s free-text preferences to books using vector similarity and optional tone/category filters. It ships with a simple Gradio UI and reproducible notebooks for data exploration, text classification, and vector search.

✨ Features
Semantic search over book descriptions (embeddings + cosine similarity)

Filters by category and/or emotion/tone (happy, suspenseful, etc.)

Fast local run with SentenceTransformers (no API required), or cloud embeddings (OpenAI) if you prefer

Interactive UI built with Gradio

Quickstart
1) Clone
bash
Copy
Edit
git clone https://github.com/Yogeshwar-Sapkal/LLM-Book-Recommender.git
cd LLM-Book-Recommender
2) Local embeddings — no API key
bash
Copy
Edit
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -U pip

3) Run the app
bash
Copy
Edit
python gradio-dashboard.py
Open the local URL Gradio prints (usually http://127.0.0.1:7860).

How it works
Load data from the provided CSVs (e.g., books.csv, books_with_categories.csv, books_with_emotions.csv).

Embed book descriptions with your chosen encoder (SentenceTransformers locally, or OpenAI).

Query is embedded the same way; we compute cosine similarity to find nearest neighbors.

Filter/sort results by category and/or emotion when requested.

Display cover image and key fields in a compact Gradio interface.

The notebooks (data-exploration.ipynb, sentiment-analysis.ipynb, vector-search.ipynb) document the analysis steps behind the UI. 
GitHub

Repository structure
pgsql
.
├─ gradio-dashboard.py           # Gradio UI
├─ books.csv
├─ books_cleaned.csv
├─ books_with_categories.csv
├─ books_with_emotions.csv
├─ data-exploration.ipynb
├─ sentiment-analysis.ipynb
├─ text-classifcation.ipynb     
├─ vector-search.ipynb
├─ tagged_description.txt
├─ cover-not-found.jpg
└─ .env                         

Configuration
Embedding choice

Local: sentence-transformers/all-MiniLM-L6-v2 (default in the instructions above)

OpenAI: set OPENAI_API_KEY and EMBEDDING_MODEL in .env

Data fields: The CSVs include preprocessed metadata (categories, emotions). If you change columns, adjust the loader logic in gradio-dashboard.py.

Customization tips
Swap in a different embedding model (e.g., larger SentenceTransformers model) for better recall.

Add FAISS or ChromaDB for persistent indexing if your dataset grows.

Extend filters (e.g., author, year, language).

Cache embeddings on disk so you don’t recompute every run.

Troubleshooting
No results / poor matches: Ensure descriptions are non-empty; try a larger model or normalize text.

API errors (OpenAI): Check your .env values and rate limits.

Unicode/CSV issues: Open files with encoding="utf-8" and ensure consistent separators.

Credits & data
The project includes CSVs produced during the notebooks’ preprocessing steps. If you incorporate third-party data sources later, document licenses and attributions here.

Cover placeholders use cover-not-found.jpg. 
GitHub

License
No license file is included yet. Add one (e.g., MIT) if you intend others to use/modify this work.

Roadmap
 Persisted vector index (FAISS/ChromaDB)

 Re-ranker (e.g., cross-encoder) for higher precision

 Dockerfile + requirements.txt for one-click setup

 Optional RAG chat mode to explain why a book matches
