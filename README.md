# 🛒 Retail Sales Performance Dashboard (2009–2011) — Power BI  
[![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)]()
[![Power BI](https://img.shields.io/badge/Power_BI-DAX-F2C811?logo=power-bi&logoColor=white)]()
[![pandas](https://img.shields.io/badge/pandas-Data_Cleaning-150458?logo=pandas)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Includes KPIs and dynamic business visualizations built with **Python (ETL)** and **Power BI (DAX + visuals)**.

---

## 🎬 Dashboard Demo
<p align="center">
  <img src="powerbi/Retail_Sales_Performance_Dashboard_(2009–2011)_GIF.gif" width="90%" alt="Retail Dashboard demo animation">
</p>

---

## 📖 Project Overview

This project showcases the complete **Data Analytics workflow**:  
> **ETL (Python + pandas) → Clean CSVs → Power BI Dashboard (DAX + Visuals)**  

Dataset: [Online Retail II (UC Irvine)](https://archive.ics.uci.edu/dataset/502/online+retail+ii) — transactions from 2009–2011.

---

## 📂 Project Structure

retail-etl-powerbi/
├─ data/
│ ├─ raw/
│   └─ README.md # Original dataset (not uploaded)
│ ├─ processed/
│   └─ processed.zip
├─ etl/
│ └─ 01_etl_retail.ipynb
├─ powerbi/
│ ├─ Retail_Sales_Performance_Dashboard_(2009–2011).pbix
│ ├─ Retail_Sales_Performance_Dashboard_(2009–2011).png
│ └─ Retail_Sales_Performance_Dashboard_(2009–2011)_GIF.gif
├─ requirements.txt
├─ .gitignore
└─ README.md


---

## ⚙️ ETL Pipeline (Python)

### 🔹 Transformations performed in `01_etl_retail.ipynb`
- Removed duplicates, null values, and invalid transactions  
- Filtered negative quantities for returns  
- Added new fields:
  - `LineTotal = Quantity × UnitPrice`
  - `IsReturn` (flag)
  - `InvoiceDateKey`, `InvoiceYear`, `InvoiceMonth`
- Exported processed datasets (`fact_sales`, `dim_product`, `dim_customer`)

---

## 📊 Power BI Dashboard

### 🖼️ Dashboard Preview
![Dashboard](powerbi/Retail_Sales_Performance_Dashboard_(2009–2011).png)

### 📈 Main KPIs
| KPI | Description |
|-----|--------------|
| 💰 **Net Revenue** | Total sales minus returns |
| 🧾 **Orders** | Distinct invoices without returns |
| 👥 **Active Customers** | Unique customers per period |
| 📦 **AOV** | Average order value (Revenue ÷ Orders) |
| 🔁 **Return Rate** | % of sales returned |

---

## 🧮 DAX Measures

```DAX
Total Amount = SUM ( fact_sales[LineTotal] )

Sales = CALCULATE ( [Total Amount], fact_sales[IsReturn] = FALSE() )
Returns = CALCULATE ( -[Total Amount], fact_sales[IsReturn] = TRUE() )
Net Revenue = [Sales] - [Returns]

Orders = CALCULATE ( DISTINCTCOUNT ( fact_sales[InvoiceNo] ), fact_sales[IsReturn] = FALSE() )
AOV (Average Order Value) = DIVIDE ( [Sales], [Orders] )
Return Rate = DIVIDE ( [Returns], [Sales] )

Active Customers =
CALCULATE ( DISTINCTCOUNT ( fact_sales[CustomerID] ), fact_sales[IsReturn] = FALSE() )

--DATA TABLE--
Date =
ADDCOLUMNS (
    CALENDAR ( MIN ( fact_sales[InvoiceDate] ), MAX ( fact_sales[InvoiceDate] ) ),
    "Year", YEAR ( [Date] ),
    "MonthNum", MONTH ( [Date] ),
    "Month", FORMAT ( [Date], "MMM" ),
    "YearMonth", FORMAT ( [Date], "YYYY-MM" ),
    "Quarter", "Q" & FORMAT ( [Date], "Q" )
)
```

---

## 💡 Key Insights

$19M total revenue between 2009–2011
United Kingdom leads all sales regions
~7% return rate, consistent across years
Top products belong to home decoration and gifting categories

---

## 🎨 Dashboard Features

✨ Clean modern layout (light theme)
📊 Dynamic KPI cards & interactions
📍 Geographic revenue map (Bing Maps)
🧮 Reusable DAX measures & star schema model

---

## 🧠 Tech Stack

| Area          | Tools Used                             |
| ------------- | -------------------------------------- |
| Data Handling | Python, pandas, openpyxl, pyarrow      |
| Dashboarding  | Power BI, DAX, Star Schema Modeling    |
| Visualization | Power BI Charts, Maps, Cards, Tooltips |
| Environment   | Jupyter Notebook, GitHub Repository    |

---

##  ▶️ Reproducibility

1️⃣ Download or clone this repository
2️⃣ Place online_retail_II.xlsx inside /data/raw/
3️⃣ Run /etl/01_etl_retail.ipynb to generate clean CSVs
4️⃣ Open the .pbix file in Power BI Desktop
5️⃣ Connect to /data/processed/ for your local paths

---

## 🧩 Next Steps

✅ Add Year-over-Year comparison visual
✅ Automate ETL via Python script
✅ Expand with profitability metrics & forecasting

---

Mónica Venzor
📍 Data Analyst Jr | SQL | Excel | Power BI | Python | Data Visualization | Machine Learning Enthusiast
🔗[LinkedIn](https://www.linkedin.com/in/monicavenzor/) |  — [GitHub](https://github.com/MonicaVenzor)  
---

## 📜 License

This project is licensed under the MIT License — free for educational and personal use.

---
⭐ If you found this project useful or inspiring, please give it a star!
It helps others discover it and supports more open projects like this 💫
---
