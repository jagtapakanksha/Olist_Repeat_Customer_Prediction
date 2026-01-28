# Olist_Repeat_Customer_Prediction

End-to-end Databricks Lakehouse project to predict repeat customers using **PySpark** and **MLflow**.

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Databricks-red?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Storage-Delta%20Lake-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/ML-PySpark-orange?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Tracking-MLflow-green?style=for-the-badge"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Architecture-Medallion-brightgreen"/>
  <img src="https://img.shields.io/badge/Domain-E--Commerce-lightgrey"/>
</p>

---

## Project Overview

Dataset: Olist Brazilian E-Commerce Public Dataset (https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

This project builds a **production-style end-to-end analytics and machine learning pipeline** on Databricks using the **Olist e-commerce dataset**.

The objective is to **predict whether a customer will make a repeat purchase** based on historical order behavior and customer-level features.

The project follows **industry-standard Lakehouse principles** and demonstrates how **data engineering and machine learning integrate in real-world systems**.

---

## Business Problem

Customer retention is a key growth driver in e-commerce.

### Problem Statement
**Can we predict whether a customer will return for another purchase using past transaction behavior?**

### Business Impact
- Identify high-probability repeat customers
- Target retention campaigns effectively
- Reduce unnecessary marketing spend

---

##  Architecture Overview  
**Databricks Medallion Architecture**

<img width="1024" height="1536" alt="Architecture" src="https://github.com/user-attachments/assets/2163ad76-8ff6-40ac-8a1e-c107bb7e9210" />

---

## Bronze Layer — Raw Data Ingestion

**Purpose:** Preserve raw data exactly as received.

### Datasets Ingested
- Customers  
- Orders  
- Order Items  
- Payments  
- Products  

### Key Characteristics
- No filtering or transformations
- Schema inferred automatically
- Stored as Delta tables

Bronze layer ensures **traceability and replayability**

---

## Silver Layer — Data Cleaning & Aggregation

**Purpose:** Apply business logic and prepare analytical datasets.

### Key Transformations
- Filtered only *delivered* orders
- Joined orders, customers, and payments
- Aggregated data at customer level

### Output Table
`silver_customer_summary`
- `total_orders`
- `total_spent`

Silver layer produces **clean and reliable customer metrics**

---

## Gold Layer — Feature Engineering

**Purpose:** Build ML-ready business features.

### Features Created

| Feature           | Description               |
|-------------------|---------------------------|
| `total_orders`    | Total orders per customer |
| `total_spent`     | Lifetime spend            |
| `avg_order_value` | Average spend per order   |
| `repeat_customer` | Target label              |

### Label Definition
repeat_customer = 1 if total_orders > 1 else 0

Final Table: **`gold_customer_features`**

---

## Machine Learning Layer

**Objective:** Predict repeat customers using behavioral data.

### Model Details
- Algorithm: Logistic Regression  
- Framework: PySpark ML  
- Train/Test Split: 80/20  

### Input Features
- Total orders  
- Total spend  
- Average order value  

### Target
`repeat_customer`

---

## Model Evaluation

The dataset is **highly imbalanced**, making accuracy misleading.

### Metrics Used
- ROC-AUC  
- Weighted Precision  

### Why Precision Matters
- Marketing actions cost money
- False positives lead to wasted spend
- High precision = smarter targeting

---

## Experiment Tracking with MLflow

MLflow is used for **reproducibility and experiment governance**.

### Logged Artifacts
- Trained model
- ROC-AUC score
- Precision score

Aligns with **production ML best practices**

---

## Key Insights
- Repeat customers form a small fraction of the user base
- Behavioral features still provide predictive value
- Lakehouse + ML architecture scales well for real systems

### Model Limitations
- Severe class imbalance
- Limited behavioral features
- Default classification threshold

### Future Improvements
- Add recency & frequency features
- Include delivery time and review scores
- Apply class imbalance handling
- Threshold optimization
- Explore tree-based models

---

## Tech Stack

| Category   | Tools        |
|------------|--------------|
| Platform   | Databricks   |
| Storage    | Delta Lake   |
| Processing | Apache Spark |
| ML         | PySpark ML   |
| Tracking   | MLflow       |
| Language   | Python       |

---

## Conclusion

This project demonstrates how to design a **scalable, production-ready data & ML pipeline** using modern Lakehouse principles.

It bridges:
- Data engineering  
- Feature engineering  
- Machine learning  
- Experiment tracking  

---

## Author

**Akanksha Jagtap**  
Data Analyst | Data Enthusiast  
