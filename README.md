# 🛒 DataCart — E-Commerce Analytics

> An end-to-end Data Analytics project built using **ChatGPT as an AI Data Analyst assistant**, from raw data profiling and cleaning to data modeling, analysis, and dashboard development.

---

## 🎯 Project Overview

**DataCart** is an e-commerce analytics project created to demonstrate how **AI can assist a Data Analyst throughout the complete analytics workflow**.

### Workflow

![image](https://github.com/i-ashish-07/AI-Analysis/blob/main/my_data_analytics_project_workflow_with_previous_flow.drawio%20(1).png)

---

## 📂 Dataset Overview

| Dataset             |   Rows | Description                              |
| ------------------- | -----: | ---------------------------------------- |
| `orders_raw.csv`    | 25,050 | Order transactions, sales, cost & profit |
| `customers_raw.csv` |  2,010 | Customer information                     |
| `products_raw.csv`  |    100 | Product, category & pricing information  |
| `regions_raw.csv`   |     20 | Region, state & city information         |

### 🔍 Data Quality Issues

| Dataset   | Issue                                 | Count / Details |
| --------- | ------------------------------------- | --------------: |
| Orders    | Exact duplicate transactions          |              50 |
| Orders    | Invalid/missing order dates           |              10 |
| Orders    | Missing customer IDs                  |              60 |
| Orders    | Missing product IDs                   |              35 |
| Orders    | Negative quantities                   |              15 |
| Orders    | Negative sales values                 |              15 |
| Orders    | Negative profit records               |             586 |
| Customers | Duplicate customer records            |              10 |
| Products  | Category naming inconsistencies       |        Multiple |
| Products  | Category/Sub-category inconsistencies |  12 corrections |

---

# 🤖 AI-Assisted Workflow

The main purpose of this project was to explore:

> **How can ChatGPT assist a Data Analyst in transforming raw business data into a complete analytical solution?**

---

# 🧹 AI-Assisted Data Cleaning Principles

A key principle of this project was that **AI should not blindly modify or delete data**.

### 1. Never Delete Duplicates Immediately

Duplicates should first be **identified and flagged**, not automatically deleted.

The workflow was:

`Detect → Flag → Investigate → Understand → Decide → Clean`

For example:

* Identify all duplicate rows.
* Flag the duplicates.
* Check whether they are exact duplicates or legitimate repeated transactions.
* Understand the business context.
* Only then decide whether to remove them.

In this project, the **50 duplicate order transactions** were identified and validated before removal.

---

### 2. Flag Missing Values Before Handling Them

Missing values should not automatically be replaced with zero, averages, or other values.

The workflow was:

`Detect → Flag → Understand → Apply Business Context → Clean`

Examples:

* Missing customer ID
* Missing product ID
* Missing order date

The appropriate treatment depends on how the missing value affects the business analysis.

---

### 3. Negative Values Should Be Investigated

Negative values do not automatically mean the data is incorrect.

For example, a negative quantity may represent a **product return**.

Instead of deleting these transactions, an `is_return` flag was created.

```text
Negative Quantity
       ↓
is_return = TRUE
       ↓
Return Transaction
```

This preserves the original transaction and allows returns to be analyzed separately.

Negative profit was also retained because it can represent a **genuine loss-making transaction**.

---

### 4. Cleaning Decisions Should Follow Business Context

Before changing data, the analysis should ask:

* Is this actually an error?
* Could this represent a legitimate business event?
* Can the correct value be determined?
* Should it be removed?
* Should it be flagged?
* Should it be imputed?
* What impact will the decision have on the analysis?

> **Flag first → Understand the business context → Validate → Then clean.**

---

# 💬 Prompts & ChatGPT Outputs

## 1️⃣ Project Setup & Data Profiling

### Prompt

> I am building a Data Analyst portfolio project called "DataCart". The goal is to demonstrate how AI can assist a Data Analyst in going from raw business data to an analytical data model and eventually to an interactive dashboard. Inspect the datasets, understand the business scenario, identify the grain, keys, relationships and all data-quality issues. Do not modify the data yet. First profile and flag duplicates, missing values, invalid values, inconsistent categories and other quality issues. Then propose an end-to-end analytics workflow.

### ChatGPT Output

* Identified dataset structure and table grain.
* Identified primary and foreign key relationships.
* Profiled missing values and duplicates.
* Identified invalid dates and negative values.
* Identified inconsistent product categories.
* Recommended **flagging issues before making cleaning decisions**.
* Proposed an end-to-end analytics workflow.

---

## 2️⃣ Orders Data Cleaning

### Prompt

> Clean the orders data. First identify and flag all exact duplicate transactions, missing values, invalid dates, missing customer/product IDs and negative values. Do not automatically delete or impute anything. Explain what each issue could mean from a business perspective. Then recommend whether each issue should be removed, retained, flagged or imputed. Create an `is_return` flag for negative quantities.

### ChatGPT Output

* Found **50 exact duplicate transactions**.
* Identified **10 invalid/missing dates**.
* Identified **60 missing customer IDs**.
* Identified **35 missing product IDs**.
* Identified **15 negative quantities**.
* Created `is_return` to classify negative quantities as returns.
* Retained negative-profit transactions because they may represent genuine losses.
* Applied business context before deciding which records should be removed.

---

## 3️⃣ Customer Data Cleaning

### Prompt

> Clean the customer data. First flag all duplicate customer records, missing values and invalid values. Do not immediately delete duplicates. Determine whether they are exact duplicate records or legitimate repeated customer IDs. Based on the business context, recommend the appropriate treatment and create a clean customer dataset.

### ChatGPT Output

* Found **10 duplicate customer records**.
* Checked whether duplicates were exact copies.
* Confirmed the duplicate records.
* Removed the confirmed duplicate records after validation.
* Standardized `signup_date`.
* Validated customer IDs and missing values.

---

## 4️⃣ Product Data Cleaning

### Prompt

> Profile the product data and first flag all category and sub-category inconsistencies. Do not automatically change category values. Compare product names, categories and sub-categories, identify genuine inconsistencies, and recommend corrections based on the business taxonomy.

### ChatGPT Output

* Detected inconsistent category naming.
* Identified values such as `furniture`, `Furniture`, `electronics` and `OFFICE SUPPLIES`.
* Validated category/sub-category relationships.
* Identified **12 products requiring category corrections**.
* Standardized the product taxonomy after validation.

---

## 5️⃣ Data Modeling

### Prompt

> Based on the cleaned e-commerce datasets, design a proper star schema. Identify the fact table, dimension tables, primary keys, foreign keys, relationships, grain and recommended date dimension.

### ChatGPT Output

Designed a **Star Schema** consisting of:

* `FactOrders`
* `DimCustomer`
* `DimProduct`
* `DimRegion`
* `DimDate`

<img width="1687" height="1307" alt="mermaid-diagram" src="https://github.com/user-attachments/assets/24b2bf76-02ff-4a50-b88d-8bbcbfe6dcf6" />


The model separates transactional data from descriptive dimensions and supports analytical reporting.

---

## 6️⃣ Exploratory Data Analysis

### Prompt

> Perform exploratory data analysis on the cleaned e-commerce data. Analyze revenue, profit, orders, customers, products, categories, regions and monthly trends. Identify useful business questions and potential business problems.

### ChatGPT Output

Analyzed:

* Revenue and profit
* Monthly trends
* Category performance
* Regional profitability
* Top products
* Customer metrics
* Product profitability
* High-revenue / low-profit performance

---

## 7️⃣ Business Problem Analysis

### Prompt

> Analyze the cleaned e-commerce dataset for business problems such as high revenue but low profit, product performance, regional profitability and category performance. Use appropriate thresholds and explain the business meaning of the results.

### ChatGPT Output

* Identified top-performing products.
* Compared revenue and profit.
* Analyzed regional profitability.
* Compared category performance.
* Investigated high-revenue but relatively low-profit products.
* Translated analytical findings into business-focused questions.

---

## 8️⃣ Dashboard Development

### Prompt

> Create a professional interactive dashboard using the cleaned DataCart data. It should include Year, Region and Category filters, KPI cards, monthly revenue/profit trend, revenue by category, profit by region and Top 10 products.

### ChatGPT Output

Designed an interactive dashboard containing:

* Total Revenue
* Total Profit
* Total Orders
* Total Customers
* Profit Margin
* Monthly Revenue & Profit Trend
* Revenue by Category
* Profit by Region
* Top 10 Products
* Year, Region and Category filters

[![Demo Preview](screenshot.png)](file:///C:/Users/ashis/Downloads/vibe_analysis_dashboard%20(1).html)



---

# 🧠 Key Learning

This project demonstrates that **AI should assist the analyst, not blindly make data decisions**.

The most important principle followed throughout the project was:

> **Flag first → Understand the business context → Validate → Then clean.**

ChatGPT helped identify issues and recommend possible treatments, while the final cleaning decisions were based on **data validation and business context**.

### ChatGPT assisted with:

* Data profiling
* Data-quality detection
* Duplicate investigation
* Missing-value handling
* Business-rule validation
* Feature creation
* Exploratory analysis
* Business problem identification
* Data modeling
* Dashboard development

---

## 🛠️ Tool Used

**ChatGPT** — Used as an AI Data Analyst assistant throughout the project.

---

> **AI can accelerate the Data Analyst workflow, but good analysis still requires human validation, business context and analytical judgment.**
