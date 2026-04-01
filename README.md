# COMP 3610 Assignment 3 - LLM-Powered Applications & Distributed Computing

This notebook covers two parts: distributed data processing with PySpark, a RAG pipeline over TLC documents.

## Requirements

Install all dependencies before running:

```
pip install -r requirements.txt
```

Java (JDK 17) is required for PySpark. Make sure `JAVA_HOME` is set correctly on your machine. If you are on Windows, you will also need Hadoop binaries and `HADOOP_HOME` set. The commented-out lines at the top of the imports cell show the expected paths - uncomment and update them to match your setup.

## Environment Variables

Create a `.env` file in the project root with the following:

```
LLM_BASE_URL=your_openai_compatible_base_url
LLM_API_KEY=your_api_key
LLM_MODEL=your_model_name
```

The notebook loads these automatically via `python-dotenv`.

## Folder Structure

```
docs/              - TLC PDF documents used for the RAG pipeline
data/raw/          - taxi parquet file is downloaded here automatically
data/partitioned/  - written by the Spark partitioning task
chroma_db/         - created automatically when the vectorstore is built
```

The taxi dataset (`yellow_tripdata_2024-01.parquet`) is downloaded automatically from the NYC TLC public URL on first run. Subsequent runs skip the download if the file already exists.

Do not commit `data/`, `chroma_db/`, or `__pycache__/` to the repository.

## Running the Notebook

Run cells top to bottom in order. The notebook is structured as follows:

Part 1 sets up a local Spark session, downloads and profiles the taxi dataset, cleans and engineers features, then runs Spark SQL queries and optimization experiments.

Part 2 loads PDFs from the `docs/` folder, chunks and embeds them using `all-MiniLM-L6-v2`, stores them in ChromaDB, and evaluates the RAG pipeline against a set of test cases.

## AI Disclosure

AI tools (Gemini, Copilot) were used to assist with development of this assignment such as creating prompts and testing (Gemini was use for Part 2).
