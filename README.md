# 💰 Azure Crypto Currency Data Pipeline

This project builds a full data pipeline using Azure tools to fetch and analyze daily closing prices of selected cryptocurrencies (BTC, ETH, DOGE, USDT, XRP) and share results via a Power BI dashboard.

---

## 📊 Features

- ✅ Pulls crypto prices daily from [Alpha Vantage API](https://www.alphavantage.co/)
- ✅ Stores raw API JSON into Azure Data Lake (bronze layer)
- ✅ Runs Databricks notebooks for transformation and enrichment (silver & gold layers)
- ✅ Outputs clean CSV for Power BI dashboard (public access)
- ✅ Scheduled daily using Azure Data Factory & Databricks Jobs
- ✅ Sends email alerts on pipeline success/failure (via Azure Monitor)

---

## 🧰 Tools Used

| Layer       | Tool / Tech                        | Purpose                         |
|-------------|------------------------------------|---------------------------------|
| Ingestion   | Azure Data Factory                 | API calling + storage           |
| Storage     | Azure Data Lake Gen2               | Bronze/Silver/Gold layer store  |
| Processing  | Azure Databricks (PySpark)         | Data transformation             |
| Scheduling  | ADF Trigger + Databricks Notebook  | Daily automation                |
| Analytics   | Power BI (Publish to Web)          | Visualization                   |
| Monitoring  | Azure Monitor + Alerts             | Email on success/failure        |
| Versioning  | GitHub                             | Code & pipeline version control |

---

## 🔄 Pipeline Overview

1. `datafactory/pipeline/crypto_bronze_pipeline.json`:  
   Fetches data for 5 cryptocurrencies using a `Lookup` + `ForEach` + `Copy Data` loop.

2. `databricks/notebooks/`:
   - **silver_layer_transformations.py**: Cleans & flattens raw JSON → CSV
   - **gold_layer_transformations.py**: Adds enrichments like rolling avg, % change, spike flag

3. Output is merged into:
   Since CSV file `gold_merged.csv` to be used for visualizations which is accessible via public Power BI link.

---

## 📅 Daily Schedule

- **ADF pipeline** is scheduled to run every day at 08:00 UTC
- Upon success, it triggers Databricks notebooks for silver and gold transformations

---

## 📬 Email Alerts

Email notifications are sent for:
- ✅ Pipeline success
- ❌ Pipeline failure  
via Azure Monitor + Log Analytics + Action Group setup.

---

## 📎 How to Use

### 🔧 Prerequisites:
- Azure Subscription
- Azure Storage Account (with ADLS Gen2)
- Azure Data Factory & Azure Databricks
- Alpha Vantage API Key

### 🔑 Config Files to Customize:
- `datafactory/parameters/crypto_list.json`
- `databricks/notebooks/*.py` (paths and tokens)
- `.env` file (not included here) for secure key handling

---

## 🔗 Power BI Dashboard

You can view the screenshot here.

---

## 🙌 Contributions Welcome

If you'd like to contribute improvements, new features, or support for other data sources, feel free to open a PR or discussion.

---

## 📜 License

MIT License
