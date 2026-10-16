# Banking Data Projects

A set of small, runnable projects that use **synthetic banking data**. No real customer data is included. Each project has its own dataset, notebook or app, and documentation, so it can be run on its own.

## Projects

| Project | What it shows | Start here |
|---|---|---|
| **Bank data pipeline** (pandas and PySpark) | ETL on a raw transaction feed: profiling, cleaning, validation, quarantine with reason codes, reconciliation, and medallion (bronze, silver, gold) layers | `bank_data_pipeline.ipynb`, `bank_data_pipeline_spark.ipynb` |
| **Agentic banking pipeline** | Prepares banking data for an LLM agent: masked customer data, account-month briefs, a TF-IDF search index, typed tools, an offline router or optional Claude agent, and guardrails | [`agentic_project/README.md`](agentic_project/README.md) |
| **Suspicious-transaction explainer** | An AML review tool: explainable rules and weighted scores, a draft analyst note with a number guardrail, and a browser app with decisions, an audit trail and CSV export | [`suspicious_explainer/README.md`](suspicious_explainer/README.md) |
| **Charts** | Three charts from the Spark pipeline output, with the script that draws them | `charts/make_charts.py` |

## Files in this folder

| File or folder | Purpose |
|---|---|
| `bank_data_pipeline.ipynb` | pandas pipeline notebook. Every code line has a comment |
| `bank_data_pipeline_spark.ipynb` | PySpark pipeline notebook (bronze, silver and gold Parquet layers) |
| `executed_bank_data_pipeline.ipynb`, `executed_bank_data_pipeline_spark.ipynb`, `executed_bank_data_pipeline_spark.html` | Copies of the notebooks with their outputs saved, so you can read the results without running them |
| `bank_pipeline_demo.mp4` | Slideshow demo of the pipeline |
| `bank_pipeline_notebook_run.mp4` | Recording of the notebook code running, with its real outputs |
| `charts/` | `1_quarantine_reasons.png`, `2_channel_summary.png`, `3_net_flow_by_account.png`, and `make_charts.py` |
| `agentic_project/` | Agentic banking pipeline: notebook, dataset, generator script, README and demo video |
| `suspicious_explainer/` | Suspicious-transaction explainer: notebook, analyst app, dataset, scripts, screenshots, demo video and README |
| `suspicious_explainer.zip` | The suspicious-transaction explainer, packed for download |

## Running the projects

**Bank data pipeline (pandas):** put `bank_transactions.csv` and the notebook in one folder, run `pip install pandas numpy`, then run all cells. Results are written to `output/`.

**Bank data pipeline (PySpark):** install Java 17 or 21, then `pip install pyspark pandas`. Run all cells. Parquet layers go to `lakehouse/` and CSV extracts to `output_spark/`.

**Agentic pipeline and suspicious-transaction explainer:** see each project's README.

**Charts:** run `charts/make_charts.py` after the PySpark notebook has written `output_spark/`.

## Data and privacy

- All datasets are synthetic. Account, transaction and customer IDs are invented.
- Customer IDs are masked with salted SHA-256 tokens before they are written to any file an LLM or the app can read. Masking is not anonymisation. Change the salt before sharing.
- Currency conversions in the suspicious-transaction explainer use a fixed demo rate, not a market rate.

## Known limitations

- The pipelines rebuild their outputs on each run. They are not incremental.
- The PySpark notebook runs on one machine by default.
- The business rules are simple examples. Real banks use many more controls.
- The optional Claude steps have not been tested against the live API.
