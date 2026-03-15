# 🚕 NYC City Taxi: Automated End-to-End Data Lakehouse
[![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)](https://databricks.com/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)

## 📖 Project Overview
This project implements a fully automated, scalable **Medallion Architecture** (Bronze → Silver → Gold) to process NYC Taxi trip data. The pipeline handles raw data ingestion from Web APIs, complex PySpark transformations, and centralized data governance using **Unity Catalog**.

### **The "Why" Behind the Tech:**
* **Orchestration:** Used **ADF** instead of manual runs to ensure the pipeline is production-ready and hands-free.
* **Governance:** Implemented **Unity Catalog** (replacing legacy Hive Metastore) to demonstrate modern enterprise security standards using **Managed Identities**.
* **Performance:** Utilized **Delta Lake** for ACID transactions, Time Travel, and efficient Parquet-based storage.

---

## 🏗️ Architecture Diagram
`Web API` ➔ `Azure Data Factory` ➔ `ADLS Gen2 (Bronze)` ➔ `Databricks (Silver)` ➔ `Databricks (Gold/Unity Catalog)` ➔ `Power BI`

---

## 🛠️ Tech Stack & Key Features
* **Azure Data Factory:** Orchestrates the entire flow. Includes a `ForEach` loop for dynamic ingestion and a **Delete Activity** to ensure the pipeline is **Idempotent** (safe to re-run).
* **Azure Data Lake Gen2:** Organized into 3 layers:
    * **Bronze:** Raw Parquet files directly from the source.
    * **Silver:** Cleaned data with enforced schemas and deduplication.
    * **Gold:** Business-ready Delta tables registered in Unity Catalog.
* **Databricks (PySpark):** * **Advanced Logic:** Used `recursiveFileLookup` to handle nested directory structures.
    * **Governance:** Configured **Storage Credentials** and **External Locations** to map Azure resources without hardcoding secrets.
* **GitHub Integration:** Full CI/CD setup for both ADF JSON definitions and Databricks notebooks.

---

## 🚀 Key Learning Milestones (Portfolio Highlights)
> **1. Idempotent Design:** Solved the duplication issue by implementing dynamic file naming in ADF, ensuring that re-running the pipeline overwrites existing data rather than creating duplicates.
> 
> **2. Modern Governance:** Transitioned from legacy "Service Principal Secrets" to **Unity Catalog Managed Identities**. This provides a central audit log and superior security for enterprise environments.
> 
> **3. Automated Triggers:** Configured ADF to automatically trigger Databricks notebooks upon successful data landing, reducing manual intervention to zero.

---

## 📂 Repository Structure
* **/ADF_Config**: Pipeline JSONs, Linked Services, and Dataset definitions.
* **/Databricks_Notebooks**: 
    * `Silver_Transformations.py`: Data cleaning and schema enforcement.
    * `Gold_Unity_Registration.py`: Business logic and Unity Catalog table creation.
* **README.md**: Project documentation.

---

## 🔧 Setup & Usage
1. **ADF Setup:** Import the JSONs from `/ADF_Config` and update the Linked Service connection strings.
2. **Databricks Setup:** Link your workspace to this GitHub repo and generate a Personal Access Token (PAT).
3. **Storage:** Create an ADLS Gen2 account with containers named `bronze`, `silver`, and `gold`.
4. **Run:** Trigger the `NYC_Main_Pipeline` in ADF.
