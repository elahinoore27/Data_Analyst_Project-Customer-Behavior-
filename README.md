# Customer Shopping Behaviour Analysis

An end-to-end data analytics project that turns customer-shopping records into practical business insights. The workflow covers Python-based data preparation and exploratory analysis, PostgreSQL queries, an interactive Power BI dashboard.

## Project overview

The project explores purchasing patterns, customer demographics, product performance, subscription behaviour, discount use, and shopping frequency. Its goal is to provide a clean, reproducible analysis that can support merchandising, marketing, and customer-retention decisions.

## Dataset

The source dataset contains **3,900 customer purchase records** and **18 original fields**. It includes customer attributes (such as age, gender, and location), product details, purchase amount, season, review rating, subscription status, shipping type, discounts, payment method, and purchase frequency.

During preparation, the analysis:

- checks data types, descriptive statistics, and missing values;
- fills 37 missing review ratings with the median rating within each product category;
- standardises column names to snake_case and renames `purchase_amount_(usd)` to `purchase_amount`;
- creates `age_group` quartiles and a numeric `purchase_frequency_days` field; and
- removes `promo_code_used` after confirming that it duplicates `discount_applied`.

## Tools used

| Tool | Purpose |
| --- | --- |
| Python, Pandas, Jupyter Notebook | Data loading, cleaning, transformation, and exploratory data analysis |
| PostgreSQL | Storing the prepared dataset and answering business questions with SQL |
| SQLAlchemy and psycopg2 | Loading the prepared data from Python into PostgreSQL |
| Power BI | Interactive dashboard and visual storytelling |
| Gamma | Stakeholder presentation of the project findings |

## Workflow

1. Load the CSV dataset in Python.
2. Perform exploratory data analysis and clean the data in the Jupyter notebook.
3. Create analysis-ready features, including age groups and purchase-frequency days.
4. Load the prepared dataset into PostgreSQL as the `customer` table.
5. Run SQL queries to answer targeted business questions.
6. Build a Power BI dashboard to present customer and revenue trends.
7. Summarise the insights in a written report and Gamma presentation.

## SQL analysis

The SQL file contains ten business questions covering:

- revenue by gender and age group;
- high-spending customers who used discounts;
- top-rated products and the most-purchased items by category;
- shipping-type, subscription, discount, and repeat-buyer behaviour; and
- customer segmentation into New, Returning, and Loyal groups.

All queries expect the cleaned PostgreSQL table to be named `customer`.

## Key findings

The following figures are reproducible from the supplied dataset:

- Total recorded revenue is **$233,081**, with an average purchase amount of **$59.76**.
- **Clothing** is the highest-revenue category at **$104,264** (about 45% of total revenue).
- Male customers account for **$157,890** in recorded revenue; this should be interpreted alongside the larger number of male records in the dataset.
- Subscribers and non-subscribers have very similar average purchase amounts (**$59.49** and **$59.87**, respectively), so the data does not show a clear subscriber spend advantage.

## Dashboard

The Power BI dashboard is designed to make customer and sales patterns easy to explore. It supports analysis by category, gender, age group, subscription status, shipping type, discounts, and customer purchase behaviour. 

## Project files

```text
customer-shopping-behaviour-analysis/
├── customer_shopping_behavior.csv                 # Raw customer-shopping dataset
├── Customer_shopping_Behaviour_Analysis.ipynb     # Python EDA, cleaning, and PostgreSQL load
├── customer_behavior_sql_queries.sql               # Ten PostgreSQL business queries
├── customer_behavior_dashboard.pbix                # Power BI dashboard
                                    
```

## How to run

### 1. Prepare Python

Keep the CSV and notebook in the same folder, then create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install pandas sqlalchemy psycopg2-binary jupyter
jupyter notebook
```

Open `Customer_shopping_Behaviour_Analysis.ipynb` and run the cells in order.

### 2. Prepare PostgreSQL

Start a local PostgreSQL server and create a database:

```sql
CREATE DATABASE customer_behavior;
```

Update the connection details in the notebook to match your local PostgreSQL configuration, then run the PostgreSQL-load cell. This creates or replaces the `customer` table with the cleaned dataset.

> **Security note:** Do not store passwords in the notebook or commit them to a repository. Use environment variables or a local configuration file excluded by `.gitignore`; rotate any credential that was previously saved in source code before sharing the project.

### 3. Run the SQL queries

After the `customer` table has been created, open `customer_behavior_sql_queries.sql` in pgAdmin, DBeaver, or another PostgreSQL client and run the queries. Alternatively, use:

```powershell
psql -d customer_behavior -f customer_behavior_sql_queries.sql
```

### 4. View the dashboard

Open `customer_behavior_dashboard.pbix` in Power BI Desktop. If prompted, update the data-source connection and refresh the model.

## What this project demonstrates

- End-to-end data analytics workflow, from raw CSV to stakeholder communication
- Practical data cleaning and feature engineering with Python
- Analytical SQL using aggregates, subqueries, common table expressions, and window functions
- Clear dashboarding and business storytelling with Power BI and Gamma
