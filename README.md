# Autonomous DS Crew

7-agent CrewAI pipeline that automates data science from ingestion to evaluation, generating LLM-powered reports with Groq, AutoML, ChromaDB memory, and MLflow tracking.

## What It Does
- Orchestrates a full DS workflow: ingestion, EDA, modeling, evaluation, reporting.
- Uses a vector memory (ChromaDB) to store and recall agent insights.
- Tracks experiments and artifacts locally with MLflow.
- Produces HTML/PDF reports and a cleaned dataset.

## Quickstart
1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. Set your Groq key (for example, in `.env`):
   ```bash
   GROQ_API_KEY="your_groq_api_key_here"
   ```
3. Run the pipeline:
   ```bash
   python main.py --file data/your_dataset.csv --target your_target_column
   ```

If you don't pass a file, the pipeline will run on the Iris demo dataset.

## Outputs
- Reports: `./reports`
- Models: `./models`
- Vector memory: `./chroma_db`
- MLflow runs: `./mlruns`

