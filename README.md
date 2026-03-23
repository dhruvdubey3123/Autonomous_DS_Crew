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

## LLM Usage (Model + Toggles)
- **Model**: All agents use Groq with `GROQ_MODEL` (default `meta-llama/llama-4-scout-17b-16e-instruct`).
- **Per-stage LLM**: Each agent is LLM-backed for reasoning and narrative output; core computations are tool-driven (pandas/sklearn/MLflow).
- **Final report**: LLM generates narrative sections; set `REPORT_USE_LLM=false` to skip LLM enrichment.
- **Tool-only mode**: Set `FORCE_TOOL_ONLY=true` to run stages without LLM calls.
- **Fallback**: `FALLBACK_TOOLS_ON_LLM_FAILURE=true` enables tool fallback if LLM calls fail.

## Architecture (High Level)
- **Orchestrator** coordinates 7 agents end-to-end.
- **Memory Agent** initializes ChromaDB and stores/retrieves semantic insights.
- **Ingestion → EDA → Modeling → Evaluation → Reporting** run sequentially.
- **AutoML pipeline** trains multiple models and selects the best.
- **Reporting agent** compiles results into HTML/PDF summaries.
