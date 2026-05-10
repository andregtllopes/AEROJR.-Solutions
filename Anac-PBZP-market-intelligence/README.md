# ANAC Market Intelligence: PBZP Lead Prospecting Pipeline

## 📌 Project Overview
Following the **2024 Regulatory Shift** by ANAC (National Civil Aviation Agency), traditional demand for aeronautical services underwent a significant transformation. This project was developed for **AEROJR. Solutions** to restructure the sales funnel for the **Basic Protection Zone Plan (PBZP)**. 

The pipeline automates the discovery, validation, and qualification of leads by mining government open data and cross-referencing it with the **DECEA (Department of Airspace Control)** database. It transforms a raw database of over 5,000 aerodromes into a high-precision commercial target list.

## 🛠️ Technical Pipeline
The solution is built as a robust Data Engineering pipeline divided into four main stages:

1.  **Multi-Source Data Ingestion:** Automates the loading and consolidation of three distinct ANAC databases (Public Aerodromes, Private Aerodromes, and Helipads), handling encoding and structural standardizations.
2.  **Cascading Validation Engine:** A specialized search motor that queries the **SysAGA API (DECEA)**. It implements a priority-based logic (ICAO Code → CIAD Registration → Aerodrome Name) to verify the existence of active Protection Zone Plans.
3.  **Resilient Batch Processing:** * **Checkpoint System:** Saves progress every 20 records to ensure data persistence against network instability.
    * **Politeness Policy:** Integrated `time.sleep` intervals (0.8s) to maintain stability and comply with government portal access limits.
4.  **Lead Categorization & Export:** Automatic classification of results into a structured status mapping:
    * **Qualified:** No PBZP found (High-value sales target).
    * **Unqualified:** Valid plan already exists.
    * **Review Required:** Ambiguous or multiple results requiring human intervention.

## 📊 Logic & Business Intelligence
The technical core of the project lies in its **Qualification Logic**. Instead of a simple web scraper, the engine parses JSON responses from the DECEA portal to identify "market gaps."

* **Status 0 (The Target):** Identified aerodromes with no registered plan, representing immediate commercial opportunities.
* **Status 2 (The Intelligence):** Detects documentation inconsistencies where the API returns multiple or ambiguous entries, flagging them for a specialized technical consultant.

## 💼 Business Impact
* **Efficiency:** Automated a process that would take weeks of manual searching on government portals.
* **Market Discovery:** Identified that approximately **0.11%** of the general database consists of high-probability "Qualified" leads, allowing the sales team to focus efforts where conversion is most likely.
* **CRM Integration:** The final output is optimized for **Notion/CRM** integration, including a `Card_Created` control flag to prevent lead duplication in the sales pipeline.

## 🚀 Setup & Reproducibility
The pipeline is designed to be idempotent; it can be stopped and resumed at any time without losing processed data.

### 1. Prerequisites
* Python 3.10+
* Libraries: `pandas`, `requests`, `beautifulsoup4`

### 2. Installation
```bash
pip install pandas requests beautifulsoup4
```
### 3. Data Structure
The script expects a `data/raw/` directory containing the following ANAC datasets:
* `aerodromos_privados.csv`
* `aerodromos_publicos.csv`
* `helipontos.csv`

### 4. Execution
1. Open the `anac-pbzp-market-intelligence.ipynb` notebook.
2. Run the **Environment Initialization** and **Data Consolidation** blocks to merge the datasets.
3. Execute the **Validation Engine** to begin the automated API queries against the DECEA portal.
4. The final qualified leads will be exported to `data/processed/FINAL_QUALIFIED_PBZP_MARKET_LEADS.csv`.

> [!TIP]
> **Performance & Maintenance Notes:**
> * **Execution Time:** Due to the "Politeness Policy" and the size of the ANAC database (+5,000 records), a full run may take several hours. Use the provided **Checkpoint** logic to monitor progress and resume if needed.
> * **API Limitations:** This was a **"solution of its time"**, developed as a tactical response to the lack of an official, public API for PBZP status. It relies on querying the internal endpoints of the SysAGA portal.
> * **Stability Warning:** This code may stop functioning if the DECEA/AGA portal undergoes structural changes, updates its internal API request requirements, or modifies its access policies. It is a maintenance-dependent solution that relies on the current government web structure.