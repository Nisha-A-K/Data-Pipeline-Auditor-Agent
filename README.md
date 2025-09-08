# Data Pipeline Auditor Agent for SmythOS

This project is a fully functional "Data Pipeline Auditor" agent built on the SmythOS Agent Weaver platform. It was created as part of the SmythForged program to demonstrate proficiency in building intelligent, data-centric agents for SRE and Data Engineering tasks.

The agent is designed to monitor a data pipeline (specifically from CSV files), validate data quality against a set of dynamic rules, detect statistical drift, and load clean data into a destination database, all while generating a comprehensive audit report.

## ✨ Features

-   **Dynamic Data Ingestion:** Connects to and processes data from local CSV file sources.
-   **Rule-Based Validation Engine:** Validates data against user-defined quality rules (e.g., null checks, data type validation, business logic).
-   **Statistical Drift Analysis:** (Conceptual) Includes a component to analyze incoming data against a historical profile to detect significant changes or anomalies.
-   **Automated Reporting:** Generates a clear, concise audit report summarizing the outcomes of the pipeline run (records processed, succeeded, failed).
-   **Reliable Data Loading:** Loads only the clean, validated data into a destination SQLite database.

## ⚙️ How It Works (Agent Architecture)

The agent is built using the SmythOS visual workflow, orchestrating several key components:

1.  **API Endpoint (`Pipeline Audit`):** Acts as the main trigger, receiving the source file path, destination path, and validation rules from the user.
2.  **Data Parser:** Ingests the raw CSV data and parses its structure.
3.  **Validation & Quality Checks:** A core logic module that iterates through each record, applying the user-defined rules.
4.  **Drift Analyzer:** A conceptual ML component that would analyze statistical properties of the data.
5.  **Database Connector:** Manages the connection to the SQLite database and loads the clean data.
6.  **Report Generator:** Compiles the results into a final, human-readable summary.

## 🚀 Technology Stack

-   **Platform:** SmythOS Agent Weaver
-   **Core Logic:** Python
-   **Data Handling:** CSV, SQLite
-   **Skills Demonstrated:** Data Engineering, Data Governance, Quality Assurance, SQL, and AI Agent Design.
-   **Visualization:** Power BI (for displaying the final audit report).

## 📋 Setup & Prerequisites

To test this agent, you will need two sample CSV files located in a local directory (e.g., `C:/smythos_test/`).

#### 1. `good_data.csv`

```csv
user_id,sale_amount,item_name
101,50.00,Widget A
102,120.50,Widget B
103,75.25,Widget C
 ```

#### 2. `bad_data.csv`
```csv
user_id,sale_amount,item_name
101,50.00,Widget A
,120.50,Widget B
103,-25.00,Widget C
104,15.00,Widget D
 ```

## 🤖 How to Use (Demo Script)
- The agent is tested and operated via the "Test as Chat" interface in the SmythOS platform.
- Test Case 1: The "Happy Path" (Processing Good Data)
Prompt:

Please start a comprehensive audit on a CSV file pipeline.

The source file is located at 'C:/smythos_test/good_data.csv'.
The destination is a SQLite database at 'C:/smythos_test/audit_db.sqlite'.

The data quality rules are:
1. The 'user_id' column must not be null.
2. The 'sale_amount' must be a positive number.

No special authentication is needed.

## Expected Outcome:
The agent will process all 3 records successfully, load them into the database, and report 0 failures.

## Test Case 2: The "Sad Path" (Processing Bad Data)
Prompt:
Thank you. Now please run the same audit on the file 'C:/smythos_test/bad_data.csv'.

**Expected Outcome:**
- The agent will process 4 records.
- It will identify 2 records as failed (due to a null `user_id` and a negative `sale_amount`).
- It will load the 2 clean records into the database.
- It will provide a summary of the specific validation errors.


## 💡 Future Improvements

-   **Expand Connectors:** Add support for more data sources (e.g., REST APIs, PostgreSQL, Google Cloud Storage).
-   **Advanced Validation Rules:** Implement more complex rules using regex or cross-column validation.
-   **Enhanced Alerting:** Integrate with Slack or email to send alerts when failure rates exceed a certain threshold.
