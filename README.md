# Power BI End to End Churn Analysis Portfolio Project  
**SQL + Power BI + Machine Learning | 2025**

An end-to-end churn analysis project built from scratch to demonstrate the **full data analytics workflow**:  
- 🗄️ SQL Server for ETL (Extract, Transform, Load)  
- 🤖 Python (Random Forest) for churn prediction  
- 📊 Power BI for dashboards and visual insights  

The project uses **Telecom customer churn data** containing demographics, referrals, subscribed services, payment/revenue details, and churn-related information.  

---

## 🎯 Project Objectives
1. Analyze customer data across demographics, services, and payments.  
2. Identify churn profiles and high-risk customer segments.  
3. Build a machine learning model to predict future churners.  
4. Visualize results in a professional Power BI dashboard.  

**Key Metrics:** Total Customers, Total Churn, Churn Rate, and New Joiners.  

---

## 🛠️ Project Workflow / Architecture

### 1. SQL ETL Process
- Load raw data into **SQL Server** staging table (`stg_churn`).  
- Clean data, handle nulls with `ISNULL`, and insert into production table (`Prod_Churn`).  
- Create SQL Views:  
  - `vw_ChurnData` → Churned & Stayed customers  
  - `vw_JoinData` → New joiners (input for ML model)  

### 2. Machine Learning (Python, Random Forest)
- Export SQL views into Excel (`prediction_data.xlsx`).  
- Preprocess: drop irrelevant columns, encode categorical features, map target variable (`Stayed=0`, `Churned=1`).  
- Split into train/test sets (80/20).  
- Train **Random Forest Classifier** (`n_estimators=100`).  
- Evaluate with **Confusion Matrix**, **Classification Report** (accuracy ≈ 84%), and **Feature Importance plot**.  
- Predict churn for new customers (`vw_JoinData`) → save results as CSV.  

### 3. Power BI Dashboard
- Import `Prod_Churn` table and ML predictions CSV into Power BI.  
- Transform data in Power Query (custom columns, unpivot services, sorting helpers).  
- Create measures: `Total Customers`, `Total Churn`, `Churn Rate`, etc.  
- Build two dashboards:  
  - **Executive Summary** → KPIs, churn by demographics, geography, services.  
  - **Churn Prediction** → Predicted churners, profiles, and breakdowns.  
- Applied **professional design** with custom backgrounds, consistent color scheme, and conditional formatting.  

---

## 💻 Tech Stack
- **SQL Server (SSMS)** → Database, ETL  
- **Python 3 + Jupyter Notebook** → Machine Learning (Random Forest)  
  - Libraries: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`, `joblib`  
- **Power BI Desktop** → Dashboarding & visualization  
- **Excel / CSV** → Intermediate data exchange  

---

## 📑 SQL Queries (Highlights)

### Data Exploration
```sql
SELECT Gender,
       COUNT(Gender) AS TotalCount,
       (COUNT(Gender) * 100.0 / (SELECT COUNT(*) FROM stg_Churn)) AS Percentage
FROM stg_Churn
GROUP BY Gender;
```
## View Creation
```sql
CREATE VIEW vw_ChurnData AS
SELECT * FROM Prod_Churn WHERE Customer_Status IN ('Churned', 'Stayed');

CREATE VIEW vw_JoinData AS
SELECT * FROM Prod_Churn WHERE Customer_Status = 'Joined';

```
## 🤖 Machine Learning Model

### Overview
- **Algorithm:** Random Forest Classifier (`n_estimators=100`, `random_state=42`)  
- **Notebook:** `notebooks/churn_prediction.ipynb` (full code + explanations)

### Data preparation
- **Training source:** `vw_ChurnData` (churned & stayed)  
- **Prediction source:** `vw_JoinData` (new joiners)  
- Drop columns not used for training (e.g., `Customer_ID`, `Churn_Category`, `Churn_Reason`).  
- Encode categorical features using `LabelEncoder`.  
- Map target: `Stayed → 0`, `Churned → 1`.  
- Train/test split: **80% train / 20% test** (`random_state=42`).

### Training (example)
```python
from sklearn.ensemble import RandomForestClassifier

rf_model = RandomForestClassifier(n_estimators=100, random_state=42)
rf_model.fit(X_train, y_train)
```
### 📊 Power BI Dashboard
**Executive Summary**
-KPIs: Total Customers, New Joiners, Total Churn, Churn Rate
-Churn by: Gender, Age Group, Tenure, Contract, Payment Method, Internet Type
-Churn by Geography (Top 5 states)
-Service usage matrix (churn by services subscribed)
---
### Churn Prediction
-Total predicted churners (from ML model)
-Customer breakdown: ID, Revenue, Refunds, Referrals
-Demographic splits (Age, Gender, Marital Status)
-Profiles by Contract, Tenure, Payment Method, State
---
