# Global-Financial-Performance-Dashboard  
<img width="2048" height="1897" alt="LOGO" src="https://github.com/user-attachments/assets/98367bba-6580-4efd-9376-b78e5dc1eb1a" />

Power BI financial performance dashboard analyzing profitability, ROE, liquidity, and growth trends of top 12 companies (2009–2023)  

## 🧭 Project Introduction

This project presents a **comprehensive financial analysis** of 12 global companies using Power BI.
It combines **data modeling**, **DAX calculations**, and **interactive visualization** to evaluate each company’s performance across key financial dimensions — **profitability**, **liquidity**, **leverage**, and **growth**.
By integrating KPIs like **ROE (DuPont breakdown)**, **Revenue Growth %**, and **Debt-to-Equity Ratio**, the dashboard enables data-driven insights for strategic decision-making.  

## 🧠 Key Highlights & Learnings  

### 🔹 1. End-to-End Power BI Project Execution  

Imported and cleaned financial statements of 12 global companies (2009–2023).  
Built a **star schema model** with **Dim_Company** and **Fact_Financials** tables for optimized data relationships.  
Used **Power Query** for data transformation and custom date creation.  

### 🔹 2. Advanced DAX Formulas  

Created **KPIs and measures** such as Revenue Growth %, ROE (DuPont), Debt/Equity Ratio, and Free Cash Flow.  
Used **time intelligence functions** like DATEADD() for year-over-year comparisons.  
Applied **RANKX(), CALCULATE(), and DIVIDE()** for dynamic insights and handling missing values.  

### 🔹 3. Financial & Analytical Understanding  

Analyzed **profitability** (Net Income, Margin), **leverage, and liquidity** ratios.  
Broke down **ROE using DuPont Analysis** — understanding the effect of profit margin, asset turnover, and equity multiplier.  
Evaluated **growth performance** and long-term financial stability across companies.  

### 🔹 4. Dashboard Design & Storytelling  

Designed **6 report pages** for executive, profitability, liquidity, DuPont, growth, and company-level analysis.
Created a **consistent theme** using corporate blue and green tones for clarity and visual harmony.
Published to **Power BI Service**, creating a summary dashboard for leadership overview.

### 🔹 5. Business Insights  

Identified companies with **strong profitability and asset efficiency** driving higher ROE.  
Observed **negative investing and financing cash flows**, indicating reinvestment trends.  
Found stable **liquidity ratios** and moderate **revenue growth (~2% YoY)** across the dataset.  

### In short:
This project strengthened my ability to analyze financial data, build analytical models in Power BI, and communicate insights visually — bridging the gap between business and analytics.  
## About the Data  

The dataset used in this project contains financial statement data for 12 global companies from 2009 to 2023.
It includes key metrics used in financial analysis, performance measurement, and valuation modeling. Each record represents a company’s annual financial summary, covering profitability, liquidity, leverage, and efficiency indicators.  

### Dataset Details

**File Name**: Financial_Statements.csv  
**Columns**: 23  
**Granularity**: Company-Year level  
**Data Type**: Cleaned and structured tabular data    

### Key Columns Explained  
### Column Name:    	                           Description  
**Company:**	                                   Name of the company  
**Year**:	                                    Fiscal year (2010–2024)  
**Revenue (in B USD)**:	                      Total annual revenue in billion USD  
**Net Income (in B USD)**	:                    Net profit after tax  
**Total Assets (in B USD)**:	                  Total assets held by the company  
**Total Liabilities (in B USD)**:	            Total debt and obligations  
**Equity (in B USD)**:	                        Shareholders’ equity  
**Current Assets / Liabilities**:	            Used to calculate current ratio  
**Market Cap (in B USD)**	:                    Market capitalization value  
**ROE / ROI / ROA	Return metrics** :           indicating profitability and efficiency  
**Profit Margin %**	:                          Percentage of profit earned from revenue  
**Free Cash Flow per Share**	:                Cash available to shareholders per share  
**EPS (Earnings Per Share)**	:                Profit allocated per outstanding share  
**Industry / Sector**	 :                       Classification of company by business type  


## Data Transformation in Power Query  

Before building the data model, several transformations were performed in Power Query to clean, standardize, and prepare the dataset for analysis.

### 🧹 Steps Performed  
  
**(1) Data Cleaning**  
Removed duplicates and unnecessary columns.  
Replaced null or missing values with 0 or "N/A" where applicable.  
Standardized column names for consistency (e.g., Revenue, NetIncome, TotalAssets).  

**(2)Data Type Correction**  
Converted numeric columns (like Revenue, Assets, Liabilities) to Decimal Number type.  
Converted text-based columns (like Company Name, Sector, Industry) to Text type.  
Ensured date-related fields were properly formatted as Date type.  

**(3)Currency and Percentage Formatting**
Kept numeric values (like Revenue, Market Cap, Cash Flow) without $ signs for accurate DAX calculations.  
Converted ratios (like ROE, ROI, Profit Margin) into percentage format during visualization instead of transformation.  

**(4)Date Table Creation**

Added a custom column in Fact_Financials using formula:  
``` DAX
#date([Year], 12, 31)
```
This represents each company’s year-end date.  
Created a separate Dim_Date table for **time intelligence** (Year, Quarter, Month, etc.).  

**(5)Merging & Relationship Preparation**
Ensured CompanyName in Fact_Financials matched with Dim_Company.
Verified that each relationship key was unique in the dimension tables.

**(6)Calculated Columns**  
(i)
``` DAX
Revenue to Equity = 
DIVIDE('Financial Statements'[Revenue], 'Financial Statements'[Share Holder Equity])
```

(ii)  
``` DAX
Profit Margin % = 
DIVIDE('Financial Statements'[Net Income], 'Financial Statements'[Revenue])
```
These columns support DuPont Analysis and other advanced KPIs.  



## 🧩 Data Modeling  

The dataset follows a Star Schema model, designed for efficient analysis in Power BI.  

### 🏛️ Tables Overview  

### Fact Table:  
**Fact_Financials** — Contains all quantitative financial metrics such as Revenue, Net Income, Assets, Liabilities, Market Cap, EPS, and more.  

### Dimension Tables:  

**Dim_Company** — Includes company-specific details like Company Name, Sector, and Industry. 
                  Created a reference of the Fact_Financials(Financial_Statements) table in Power Query, removed unnecessary columns, and kept only unique company-level details —       Company Name, Category — to form the Dim_Company table.  
                  
**Dim_Date** — Contains calendar attributes such as Date, Year, Quarter, and Month, used for time-based calculations.  
``` DAX
Dim_Date = CALENDAR(DATE(2009,1,1), DATE(2023,12,31))
```
``` DAX
Year = YEAR([Date])
```
``` DAX
Quarter = "Q" & FORMAT([Date], "Q")
```
``` DAX
Month = FORMAT([Date], "MMMM")
```

<img width="1436" height="687" alt="Data Modeling" src="https://github.com/user-attachments/assets/fadbb5b9-a914-4dc1-9372-4c5245daa221" />  

### 🧠 Purpose of the Model  

Enables **time intelligence calculations** such as Year-over-Year Growth, Cumulative Trends, and Averages.  
Supports **company-level performance comparison** across industries.  
Simplifies building modular KPIs such as **ROE (DuPont), Liquidity Ratios, and Revenue Rankings.** 





