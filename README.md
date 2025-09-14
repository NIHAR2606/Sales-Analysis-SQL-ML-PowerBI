Power BI End to End Churn Analysis Portfolio Project

SQL + Power BI + Machine Learning | 2024

An end-to-end churn analysis project built from scratch to demonstrate the full data analytics workflow:

SQL Server for ETL (Extract, Transform, Load)

Power BI for dashboards and visual insights

Python (Random Forest) for churn prediction

The project uses Telecom customer churn data containing demographics, referrals, subscribed services, payment/revenue details, and churn-related information.

Project Objectives

Analyze customer data across all dimensions (demographics, services, payments).

Study churn profiles to identify at-risk customer segments.

Build a machine learning model to predict future churners.

Visualize results in a professional Power BI dashboard.

Key Metrics: Total Customers, Total Churn, Churn Rate, and New Joiners.

Project Workflow / Architecture

SQL ETL Process

Load raw data into SQL Server staging table (stg_churn).

Clean data, handle nulls using ISNULL, and load into production table (Prod_Churn).

Create SQL Views:

vw_ChurnData → Churned & Stayed customers

vw_JoinData → New joiners (for ML prediction input)

Machine Learning (Python, Random Forest)

Extract SQL views into Excel (prediction_data.xlsx).

Preprocess: drop irrelevant columns, encode categorical features, map target variable (Stayed=0, Churned=1).

Split into train/test sets (80/20).

Train Random Forest Classifier (100 trees).

Evaluate using confusion matrix, classification report (accuracy ≈ 84%), and feature importance.

Predict churn for new customers (vw_JoinData) and save results to CSV for Power BI.

Power BI Dashboard

Import Prod_Churn table and ML predictions into Power BI.

Transform data in Power Query (custom columns, unpivot services, sorting helpers).

Create explicit measures (Total Customers, Total Churn, Churn Rate, etc.).

Build two dashboards:

Executive Summary → KPIs, churn by demographics, geography, services

Churn Prediction → Predicted churners, profiles, and breakdowns

Apply professional design (PowerPoint backgrounds, consistent colors, conditional formatting).

Tech Stack

SQL Server (SSMS) → Database, ETL

Python 3 + Jupyter Notebook → Machine Learning (Random Forest)
Libraries: pandas, numpy, scikit-learn, matplotlib, seaborn, joblib

Power BI Desktop → Visualization & Dashboarding

Excel / CSV → Intermediate data exchange

SQL Queries (Highlights)

Explore data distributions (Gender, Contract, State, Customer Status).

Check for nulls across all columns.

Replace nulls with defaults (e.g., ISNULL(value_deal, 'None')).

Create production table Prod_Churn.

Create views for ML and dashboards:

vw_ChurnData: Churned and Stayed customers

vw_JoinData: New joiners

Machine Learning Model

Algorithm: Random Forest Classifier (100 trees, reproducible with random_state=42)

Evaluation:

Accuracy ≈ 84%

Precision/Recall imbalance due to more “Stayed” customers than “Churned”

Key Features Driving Churn: Contract type, Internet service type, Tenure, Monthly charge

Power BI Dashboard

Executive Summary Page

KPIs: Total Customers, New Joiners, Total Churn, Churn Rate

Churn by: Gender, Age Group, Tenure, Contract, Payment Method, Internet Type

Geographic churn analysis (Top 5 states)

Service usage matrix (churn by services subscribed)

Churn Prediction Page

Total predicted churners (from ML model)

Customer-level breakdown: ID, Revenue, Refunds, Referrals

Demographic splits (Age, Gender, Marital Status)

Churner profiles by State, Tenure, Contract, Payment Method

Key Insights

Demographics: Females over 50 account for 31.5% of churn; major reason is competitor offers.

Services: Customers without Device Protection/Backup/Security churn at over 60%.

Service Quality: Even customers with internet, phone, or paperless billing churn, suggesting service issues.

High-Risk Contracts: Month-to-month contracts have churn ≈46.5%.

Revenue Impact: Churned customers represent a significant revenue loss.

Predictions: Model flagged 378 new joiners likely to churn.

How to Run / Reproduce

SQL: Run scripts in /sql/ to build db_churn, staging, production tables, and views.

Python ML: Open notebooks/churn_prediction.ipynb, run preprocessing, train RF model, and generate predictions CSV.

Power BI: Import Prod_Churn and ML predictions and refresh dashboard visuals.

Future Improvements

Balance dataset (oversampling/undersampling) to improve ML precision for churners.

Try advanced models (XGBoost, LightGBM).

Expand Power BI geographic analysis beyond top 5 states.

Deploy ML model with Flask/Streamlit for live predictions.

Author

Project inspired by Pivotalstats (YouTube).
Adapted and implemented by Nihar Nagdeve.
