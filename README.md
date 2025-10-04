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
This project analyzes **client transaction activity** across multiple payment methods, countries, and years. 
The dashboard provides insights into client growth, transaction performance, and operational risks such as failed transactions.  

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

Since the dataset was a **flat file**, Power Query was used to reshape the data. 
Lookup tables (Client, Date) were created to make the model easier to analyze.  

<img width="1005" height="592" alt="image" src="https://github.com/user-attachments/assets/5eda4c56-4499-40c1-8f4f-2c5a1d207765" />

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

## 📊 Dashboard Highlights

1. Overall Growth

Transaction Volume: $2B (+33% YoY)

Transaction Count: 6M (+33% YoY)

Success Rate: 97%

Insight: Business is growing strongly in both value and count, showing increased adoption of services.

2. Client Concentration

SwiftPay drives $584M (32%) of all transaction volume.

Other top clients: TransLink ($504M), PayFlow ($380M), FinBank ($338M).

Insight: Heavy reliance on SwiftPay creates a concentration risk if this client reduces usage.

<img width="992" height="670" alt="image" src="https://github.com/user-attachments/assets/a7ff2711-e248-4585-a508-4a2e5b640db8" />

3. Transaction Trends

Peak Volume: $177M in May

Seasonal dips: Early year (Feb) and December

Insight: Transactions show seasonality — peaks in spring and fall, lower activity in winter months.

<img width="1143" height="635" alt="image" src="https://github.com/user-attachments/assets/16e16d71-6efa-41d1-bc6b-7c55ab22c167" />


4. Transaction Failures

SwiftPay: 50K failed transactions

FinBank: 40K failed transactions

TransLink: 35K failed transactions

PayFlow: 29K failed transactions

Insight: Even with a 97% success rate, large transaction counts mean failures still represent millions in lost value.

<img width="696" height="566" alt="image" src="https://github.com/user-attachments/assets/483ab9a1-f507-4f0c-9848-2eac4720046f" />




<img width="1566" height="687" alt="image" src="https://github.com/user-attachments/assets/a69714e5-b24e-4351-acfd-0abe9019d8dc" />


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
