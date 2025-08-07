# ETLDriven-DataFlow
End-to-end Azure Data Factory project that performs ETL from multiple sources, routes files conditionally, and uses Data Flows to analyze top credit card spenders.

## 📘 Project Overview

This Azure Data Factory project demonstrates an **end-to-end pipeline** that starts with **ETL (Extract, Transform, Load)** operations from multiple sources and continues into **advanced analytics using Data Flows**.

### 🔗 Main Features:

- Connects to **two data sources** (HTTP)
- Executes **sequential copy activities**
- Stores data in **Azure Data Lake Storage Gen2**
- Conditionally routes files (e.g., Fact files)
- Performs analytics to determine:
  - **Which credit card type (Visa, MasterCard, Amex, Others)** had
  - The **highest spending per user** within a given time frame

---

## 📂 Pipeline Breakdown

### ✅ Pipeline 1: ETL Orchestration

1. **Copy Activity 1:** Pulls data from an HTTP source
2. **Copy Activity 2:** Pulls data from another HTTP source
3. **Execute Pipeline 2:** Only triggers when both copy activities succeed

📌 Result: Data from both sources lands in ADLS Gen2

---

### 🔁 Pipeline 2: Metadata & Routing

1. **Get Metadata:** Reads files from the staging folder
2. **ForEach Activity:** Iterates through file list
3. **If Condition:** Checks if a file is a "Fact" file
   - If true → moves it to a separate folder
4. **Execute Data Flow:** Triggers analytical transformation

---

## 🔬 Data Flow Logic

- Splits data based on **card type**: Visa, MasterCard, AmericanExpress, Others
- Aggregates transactions per `customer_id`
- Uses **window functions** to rank spend
- Filters to select **top spender per card**
- Combines all results using **Union**
- Outputs to a final sink

---

## 🧠 Technologies Used

- Azure Data Factory
- Data Flows
- Azure Data Lake Storage Gen2
- Get Metadata
- Copy Activity
- ForEach + If Condition
- Aggregation, Windowing, Filtering

---


## ✅ Final Outcome

> Successfully identified **top credit card spenders per customer** using a well-orchestrated ETL and Data Flow pipeline in Azure Data Factory.
