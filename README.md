# 📊 Client Activity Dashboard  

## 📑 Table of Contents  
1. [Project Overview](#-project-overview)  
2. [Dataset](#-dataset)  
3. [Tools & Skills Used](#-tools--skills-used)  
4. [KPIs & Measures](#-kpis--measures)  
5. [Dashboard Highlights](#-dashboard-highlights)  
6. [Business Impact](#-business-impact)  
7. [Recommendations](#-recommendations)  
8. [How to Use](#-how-to-use)  
9. [Next Steps](#-next-steps)  

---

## 📌 Project Overview  
This project analyzes **client transaction activity** across multiple payment methods, countries, and years. The dashboard provides insights into client growth, transaction performance, and operational risks such as failed transactions.  

The goal is to help business leaders and account managers track client health, identify growth opportunities, and reduce transaction failures.  

---

## 📊 Dataset  
- **Source**: Simulated client transaction dataset (flat file).  
- **Rows**: 6M+ transactions  
- **Columns include**:  
  - Client Name  
  - Country & Currency  
  - Payment Method (Wire, ACH, SEPA, SWIFT)  
  - Transaction Value & Count  
  - Success Rate (%) and Failed Transactions  
  - Year (FY2021–FY2024)  

Since the dataset was a **flat file**, Power Query was used to reshape the data. Lookup tables (Client, Date) were created to make the model easier to analyze.  

<img width="1155" height="692" alt="image" src="https://github.com/user-attachments/assets/5eda4c56-4499-40c1-8f4f-2c5a1d207765" />

---

## 🛠️ Tools & Skills Used  
- **Power BI**: Data modeling, DAX measures, interactive dashboards  
- **Power Query**: Data cleaning and reshaping  
- **Excel**: Initial exploration and validation  
- **Visualization Skills**: Client segmentation, transaction trend analysis, Sankey flow analysis  

---

## 📈 KPIs & Measures  
- **Transaction Volume** = SUM(Transaction Value)  
- **Transaction Count** = COUNTROWS(Transactions)  
- **Success Rate** = % of successful transactions  
- **Failed Transactions** = COUNT where Success = “No”  
- **YoY Growth** = (Current Year – Previous Year) ÷ Previous Year  

Example DAX:  
```DAX
Transaction Count = SUM(Client_Activity[Number of Transactions])
Transaction Volume = SUM(Client_Activity[Transaction Volume (USD)])

PY Volume = CALCULATE([Transaction Volume], DATEADD(DateTable[Date],-1,YEAR))

PY Transactions = CALCULATE([Transaction Count], DATEADD(DateTable[Date],-1,YEAR))

PY Success Rate = CALCULATE([Success Rate], DATEADD(DateTable[Date],-1,YEAR))

YoY% Volume = 
VAR CYVolume = [Transaction Volume]
VAR PYVolume = CALCULATE([Transaction Volume], DATEADD(DateTable[Date], -1, YEAR))
RETURN
    DIVIDE(CYVolume - PYVolume, PYVolume)

YoY% Transaction = 
VAR CY = [Transaction Count]
VAR PY = CALCULATE([Transaction Count], DATEADD(DateTable[Date],-1,YEAR))
RETURN
    DIVIDE(CY - PY, PY)

YoY% Success Rate = 
VAR CY = [Success Rate]
VAR PY = CALCULATE([Success Rate], DATEADD(DateTable[Date],-1,YEAR))
RETURN
    DIVIDE(CY - PY, PY)

CF YoY Volume = 
SWITCH(
    TRUE(),
    [YoY% Volume] > 0, "Green",
    [YoY% Volume] < 0, "Red",
    "Grey"
    )

Success Rate (%) = 
VAR SuccessRate = [Success Rate]          
RETURN IF(SuccessRate > 1, SuccessRate / 100, SuccessRate)
```


## 💡 Business Impact

Business is growing at +33% YoY, showing strong client adoption.

Client base is concentrated, with SwiftPay driving nearly a third of total activity.

High transaction failures at top clients could undermine trust and revenue.

Seasonal booking patterns can inform capacity planning and marketing timing.

## 📝 Recommendations

Diversify Clients: Reduce reliance on SwiftPay by expanding smaller accounts.

Improve Reliability: Partner with SwiftPay, FinBank, and TransLink to cut failed transactions.

Upsell Growth Accounts: Focus on TransLink and FinBank, which are growing faster than average.

Plan for Seasonality: Use seasonal insights to align staffing, infrastructure, and promotional campaigns.

## 🚀 How to Use

Clone or download this repository.

Open the Client-Activity-Dashboard.pbix file in Power BI Desktop.

Use slicers to explore by year, client, country, and payment method.

## 📌 Next Steps

Add predictive analytics to forecast client transaction growth.

Include profitability metrics (fees earned per transaction).

Automate reporting via Power BI Service with scheduled refreshes.
