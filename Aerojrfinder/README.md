# Aerojrfinder: Data Engineering & Marketing Automation

## 📌 Project Overview
**Aerojrfinder** is a Data Engineering solution developed in the second semester of 2024 to centralize and automate contact management for **AEROJR.** (Aerospace Engineering Junior Enterprise at UFMG). The project addresses the problem of historical data fragmentation by unifying records from multiple semesters (2022-2024) that were previously scattered across isolated spreadsheets.

This repository demonstrates the complete data lifecycle: from extraction and cleaning (ETL) to the final application in a marketing automation tool for prospecting alumni and former members.

## 🛠️ Technical Pipeline
The project was consolidated into a robust pipeline divided into five logical stages:

1.  **Ingestion and ETL (Extract, Transform, Load):** Automates the reading and merging of multiple CSV files, handling a complex structure of 38 original columns, including financial fields and registration data.
2.  **Object-Oriented Modeling (OOP):** Implementation of the `Membro` (Member) class to ensure data integrity and facilitate the manipulation of attributes such as `name`, `department`, `phone`, and `role`.
3.  **Normalization via Regex:** Use of Regular Expressions to standardize Brazilian phone numbers (removing special characters and ensuring the `+55` prefix), mitigating failures in integration with messaging APIs.
4.  **Deduplication and Temporal Intelligence:** Processing logic that identifies duplicate members across different semesters and retains only the most recent entry, ensuring that the role and department used in communication are up to date.
5.  **Automation Engine (WhatsApp Bot):** Integration with `pywhatkit` and `pyautogui` for batch delivery of personalized messages, simulating human behavior to avoid blocks and managing the automatic closing of browser tabs.

## 📊 Logic & Conflict Resolution
The technical differentiator of this project lies in its **Auditability**. The Duplicate Treatment Block generates a real-time log of all conflict resolutions, documenting exactly which record was updated and why (based on chronological priority).

## 💼 Business Impact
* **Market Discovery:** The tool was used to facilitate direct contact with alumni via LinkedIn and WhatsApp, allowing for the collection of insights regarding the job market and new industry pain points.
* **Intellectual Capital Management:** Organized years of junior enterprise history, transforming static spreadsheets into a dynamic database for the Marketing department.
* **Scalability:** The architecture allows new semesters to be added to the pipeline simply by inserting a new CSV into the source folder, keeping the database constantly updated.

## 🚀 Setup & Reproducibility
To ensure the code is **Self-Contained** and reproducible by third parties (without exposing the company's original sensitive data), the notebook includes a **Mock Data** generator.
* Upon running the notebook, the system detects the absence of real data and automatically generates 6 synthetic CSV files with the original AEROJR structure to demonstrate the cleaning and automation features.
