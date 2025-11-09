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

## Key Measures & KPIs Used  

``` dax
Total Revenue = SUM('Financial Statements'[Revenue])
```
``` dax
Total Net Income = sum('Financial Statements'[Net Income])
```
```dax
ROE Rank = 
RANKX(
    ALL(Dim_Company[Company ]),
    CALCULATE(AVERAGE('Financial Statements'[ROE])),
    ,
    DESC
)
```
``` dax
Profit Margin% = DIVIDE(SUM('Financial Statements'[Net Income]), SUM('Financial Statements'[Revenue]))
```
``` dax
Revenue to Equity = 
DIVIDE(SUM('Financial Statements'[Revenue]), SUM('Financial Statements'[Share Holder Equity]))
```
```dax
ROE (DuPont) = 
[Profit Margin%] * [Revenue to Equity]
```
```dax
Revenue Rank = 
RANKX(
    ALL(Dim_Company[Company ]),
    CALCULATE(SUM('Financial Statements'[Revenue])),
    ,
    DESC
```

```dax
Revenue Growth % = 
VAR LatestYear =
    MAX('Financial Statements'[Year])
VAR CurrentRevenue =
    CALCULATE(
        SUM('Financial Statements'[Revenue]),
        'Financial Statements'[Year] = LatestYear
    )
VAR PreviousRevenue =
    CALCULATE(
        SUM('Financial Statements'[Revenue]),
        'Financial Statements'[Year] = LatestYear - 1
    )
RETURN
DIVIDE(CurrentRevenue - PreviousRevenue, PreviousRevenue)
```

```dax
Net Profit Margin% = DIVIDE([Total Net Income],[Total Revenue])
```
```dax
Operating Cash Flow = SUM('Financial Statements'[Cash Flow from Operating])
```
```dax
Investing Cash Flow = SUM('Financial Statements'[Cash Flow from Investing])
```
```dax
Free Cash Flow Per Share = AVERAGE('Financial Statements'[Free Cash Flow per Share])
```
```dax
EPS = AVERAGE('Financial Statements'[Earning Per Share])
```
```dax
EBITDA Margin % = DIVIDE(SUM('Financial Statements'[EBITDA]),[Total Revenue])
```
```dax
Avg Revenue Growth % = 
AVERAGEX(
    VALUES('Financial Statements'[Company ]),
    [Revenue Growth %]
)
```
```dax
Average ROI = AVERAGE('Financial Statements'[ROI])
```
```dax
Average ROE = AVERAGE('Financial Statements'[ROE])
```
```dax
Average ROA = AVERAGE('Financial Statements'[ROA])
```
```dax
Average Debt/Equity ratio = AVERAGE('Financial Statements'[Debt/Equity Ratio])
```
```dax
Average Current Ratio = AVERAGE('Financial Statements'[Current Ratio])
```

```dax
CAGR Revenue per Company = 
VAR MinYear =
    CALCULATE(
        MIN('Financial Statements'[Year]),
        ALLSELECTED('Financial Statements'),
        VALUES('Dim_Company'[Company ])
    )
VAR MaxYear =
    CALCULATE(
        MAX('Financial Statements'[Year]),
        ALLSELECTED('Financial Statements'),
        VALUES('Dim_Company'[Company ])
    )
VAR StartRevenue =
    CALCULATE(
        SUM('Financial Statements'[Revenue]),
        'Financial Statements'[Year] = MinYear
    )
VAR EndRevenue =
    CALCULATE(
        SUM('Financial Statements'[Revenue]),
        'Financial Statements'[Year] = MaxYear
    )
VAR NumPeriods = MaxYear - MinYear
RETURN
IF(
    NumPeriods > 0 && StartRevenue > 0,
    (EndRevenue / StartRevenue) ^ (1 / NumPeriods) - 1,
    BLANK()
)
```

## 📊 Report Pages & Visualizations

The report is designed as an **executive-level financial performance dashboard**, focusing on clarity, interactivity, and real-world finance insights.
It includes **six report pages**, each highlighting a distinct aspect of corporate financial analysis.  

## 📊 Page 1: Executive Summary (C-Level View)  

### 🎯 Purpose  
This dashboard provides a high-level financial overview designed for C-level executives.  
It highlights the company’s overall revenue, profitability, leverage, and efficiency to quickly assess financial health and performance trends.  

#### 📈 Key Metrics & Visuals  
Total Revenue ($12.21M) and Total Net Income ($1.98M)  
ROE (DuPont) – 21.47%  
Average Debt-to-Equity Ratio – 0.65  
Average Revenue Growth % – 1.11%  
Total Revenue and Net Income Trend (2009–2023)  
Revenue Ranking by Company  
<img width="1263" height="709" alt="Executive Summary (C - Level View)" src="https://github.com/user-attachments/assets/91610309-dacd-45b6-b980-bb576e6e3bed" />  

#### 💡 Business Insights  
**Apple (AAPL)** leads in total revenue ($2.97M), followed by **Amazon (AMZN) and Microsoft (MSFT)**, showing strong sales and market dominance.  
The **consistent upward trend** in revenue and net income until 2021 indicates steady business growth and effective financial management.  
The **21.47% ROE** highlights effective utilization of shareholder equity in generating profits.  
A relatively low **Debt-to-Equity ratio (0.65)** suggests that most companies are not overly reliant on debt financing — a sign of financial stability.  

#### ⚠️ Drawbacks / Challenges  
Post-2021 decline in both revenue and net income suggests possible **market saturation** or external shocks (e.g., global economic downturn).  
**Low average revenue growth (1.11%)** signals that while profits are stable, expansion is limited.  
Heavy dependency on a few top performers (like AAPL and AMZN) can pose portfolio concentration risks. 

#### 🚀 Recommendations / Improvement Opportunities  
Focus on **innovation and diversification** to sustain revenue growth.    
Strengthen **cost optimization strategies** to improve profit margins amid slower growth.    
Explore **emerging markets and product lines** to counteract stagnation in mature markets.    
Monitor leverage strategies to ensure continued balance between growth and financial risk.   

## 💰 Page 2: Profitability Analysis  

### 🎯 Purpose  
The Profitability Analysis page focuses on how efficiently each company converts revenue into profit and how well it utilizes assets and investments to generate returns.
It enables financial analysts and decision-makers to evaluate operational efficiency, cost management, and return performance across multiple companies. 

#### 📊 Key Metrics & Visuals  
Profit Margin %: 16.18% (Overall average)  
Average ROI: 11.88  
Average ROA: 7.78  
Net Profit Margin % by Company – Highlights the most and least profitable firms  
EPS (Earnings Per Share) Trend by Year – Shows profitability per share over time  
Company-wise Profitability Table – Displays Total Revenue, Total Net Income, and Profit Margin %  
<img width="1292" height="712" alt="Profitiability analysis" src="https://github.com/user-attachments/assets/a0e8f0ba-1123-4d63-bca8-e13a44c31291" />  

#### 💡 Business Insights  
**Microsoft (MSFT)** leads with the highest **profit margin (28.9%)**, followed by **NVIDIA (23.26%) and Apple (22.95%)**, showcasing superior cost control and strong profit generation.    
**Earnings Per Share (EPS)** has improved significantly since 2017, peaking at **5.7 in 2023**, indicating enhanced shareholder value.    
**Consistent positive ROI and ROA** across top companies suggest effective asset utilization and investment strategies.    
**Low-performing companies** like **PCG (-1.69%)** and **SHLDQ (-3.02%)** show **negative profit margins**, signaling financial distress or operational inefficiency.  

#### ⚠️ Drawbacks / Challenges    
**Uneven profitability distribution** across companies indicates that not all firms are managing costs or revenues effectively.    
**Volatility in EPS** between 2010 and 2018 highlights periods of inconsistent earnings, possibly due to market or operational factors.    
Some companies show **negative net income**, which can impact investor confidence and long-term sustainability.  

#### 🚀 Recommendations / Improvement Opportunities  
**Review cost structures** for underperforming companies to identify inefficiencies in operations or pricing.  
**Diversify product portfolios** and enhance innovation to maintain high margins amid competition.  
**Reinvest profits** into technology and productivity improvements to sustain ROI and ROA levels.  
Implement **benchmarking and best-practice sharing** among top performers (e.g., MSFT, NVDA) to uplift weaker firms.  
















