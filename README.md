# 🚕 NYC City Taxi: Governed End-to-End Data Lakehouse
[![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)](https://databricks.com/)
[![Delta Lake](https://img.shields.io/badge/Delta_Lake-00ADFF?style=for-the-badge&logo=delta-lake&logoColor=white)](https://delta.io/)

## 📖 Project Overview
This repository implements a **Medallion Architecture** (Bronze → Silver → Gold) for the NYC Taxi dataset. The project demonstrates advanced skills in cloud data ingestion using **Azure Data Factory** and modern data governance using **Databricks Unity Catalog**.

---

## 🏗️ Architecture & Implementation
1. **Automated Ingestion:** Azure Data Factory (ADF) utilizes a `ForEach` loop and parameterized datasets to fetch monthly Parquet files from a Web API and land them into the ADLS Gen2 Bronze layer.
2. **Unity Catalog Governance:** This project implements modern enterprise security standards by using **User-Defined Storage Credentials** and **External Locations** linked to Azure Managed Identities. This ensures secure, credential-less access to data containers.
3. **Medallion Transformations:** - **Silver:** Data cleaning, schema enforcement, and partitioning.
    - **Gold:** Business-ready Delta tables registered in Unity Catalog for high-performance querying.
4. **Delta Lakehouse:** Leveraged Delta tables in the Gold layer to enable **ACID transactions** and **Time Travel** (data versioning).

---

## 📊 For Enthusiast Analysts
I believe high-quality data should be accessible for immediate discovery.
* **1-Click Connectivity:** I have provided a `databricks-NYC_TAXI_CLUSTER.pbids` file in this repository.
* **Immediate Insights:** Any enthusiast analyst can open this file in Power BI Desktop to connect directly to the governed **Gold Layer** and start building dashboards immediately.

---

## 📂 Repository Structure
* **/ADF_Config**: JSON definitions for Pipelines, Datasets, and Linked Services.
* **/Databricks_Notebooks**: 
    * `Silver_Notebook`: Data cleaning and transformation via PySpark.
    * `Gold_Notebook`: Business logic and Unity Catalog table registration.
* `databricks-NYC_TAXI_CLUSTER.pbids`: Pre-configured Power BI Data Source file.

---

## 🚀 Key Learning Milestones
* **Governance Migration:** Successfully moved away from legacy access methods to **Unity Catalog**, providing a centralized audit log and security layer.
* **Schema Management:** Handled data transformations through the layers using Spark SQL and PySpark DDL.
* **Version Control:** Fully synced ADF and Databricks workflows with GitHub for professional CI/CD management.

---

## 🔧 Setup
1. **ADF:** Import the JSON configurations and update your storage account connection strings.
2. **Databricks:** Clone this repo into your workspace via Git Folders.
3. **Governance:** Create a Storage Credential in Databricks Catalog Explorer using your Azure Access Connector.
4. **BI:** Download the `.pbids` file to visualize the Gold layer in Power BI.
