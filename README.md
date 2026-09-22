
# 📊 Superstore Executive Performance & Profitability Dashboard

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D7?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power_Query-2BAE66?style=for-the-badge&logo=databricks&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

An interactive, end-to-end multi-page Power BI reporting solution built to evaluate retail operations, diagnose severe profit leakages, track customer return dynamics, and monitor regional sales expansion.

---

## 📌 Executive Summary

Retail organizations often struggle to translate top-line sales figures into sustainable bottom-line net profit. While a business may register massive gross revenues, factors such as **aggressive discounting**, **product returns**, and **logistics delays** can severely erode profit margins.

This project delivers an interactive, analytical reporting framework to bridge this gap. By segmenting transactions by margin health, tracking regional shipping efficiency, and isolating product-level return behaviors, the dashboard equips decision-makers with actionable operational intelligence.

---

## 🎯 Key Business Questions Addressed

1. **Top-line vs. Bottom-line Disparity:** Why does **$2.30M in Total Sales** convert to only **$23.23K in Net Profit** (an overall profit margin of **1.10%**)?
2. **Impact of Returns:** Which product sub-categories drive the **$180.50K in Returned Sales**, and in which months do returns spike?
3. **Discount & Margin Erosion:** How does discount volume correlate with negative profitability ("Severe Loss") across regional markets?
4. **Regional Disparities:** Why is the **West Region** capturing the lion's share of net profit (**$19.66K / 73.19%**), while the **Central Region** struggles with low profit yield (**$2.22K / 8.26%**) despite high discount volumes?
5. **Shipping & Operations:** How do shipping delays impact overall profitability and customer satisfaction?

---

## 🏆 Key Metric Highlights (KPIs)

* **Gross Sales:** $2.30M
* **Net Sales (Adjusted for Returns):** $2.12M
* **Total Gross Profit:** $286.41K
* **Net Profit:** $23.23K
* **Overall Profit Margin:** 1.10%
* **Year-over-Year (YoY) Sales Growth:** +45.09%
* **Total Value of Returns:** $180.50K (296 recorded return incidents)
* **Top Profit-Generating Region:** West ($19.66K Net Profit, 73.2% share)

---

## 📑 Report Structure & Page Breakdown

The dashboard comprises **5 specialized reporting pages**, accessible via a cohesive left-navigation pane:

### 1. Executive Overview
* **Focus:** High-level executive scorecard.
* **Components:**
  * Core KPI cards (Total Sales, Net Sales, Total Profit, Net Profit, Margin %, YoY Growth).
  * Net Sales by Quarter & Net Sales by Category (Office Supplies leading volume).
  * Profitability segmentation (**Exceptional Profit:** $1.13M vs. **Severe Loss:** $0.32M).
  * Impact of Shipping Delays on sales volume.
  * City-level performance ranking (New York City, Los Angeles leading).
  * <img width="3075" height="1763" alt="Mini Project 2 (Power BI) - Mourine_page-0001" src="https://github.com/user-attachments/assets/3fdcefc9-ac52-4e26-a36e-16d910367776" />


---

### 2. Product Performance
* **Focus:** Granular breakdown by Category & Sub-Category.
* **Components:**
  * Net Sales distribution (Chairs, Phones, and Storage generate the highest sales).
  * Net Profit breakdown (Copiers and Paper generate highest net margins; Tables and Bookcases experience margin drain).
  * Category Profit Margins: **Technology (2.0%)** vs. **Office Supplies (1.5%)** vs. **Furniture (0.5%)**.
  * Category YoY Growth rates (Office Supplies peaking at 91.57% YoY).
  * <img width="3075" height="1763" alt="Mini Project 2 (Power BI) - Mourine_page-0002" src="https://github.com/user-attachments/assets/e7610559-2f11-41d8-aa98-664163e33f02" />


---

### 3. Returns Analysis
* **Focus:** Diagnostics on product returns and capital recovery.
* **Components:**
  * Return KPIs: $180.50K lost to returns across 296 transactions.
  * Return seasonality: Peak return volume observed in **September**, followed by **December** and **March**.
  * Vulnerable sub-categories: **Phones** and **Chairs** dominate the total returned dollar volume.
  * <img width="3075" height="1763" alt="Mini Project 2 (Power BI) - Mourine_page-0003" src="https://github.com/user-attachments/assets/32df06df-c08c-4cf9-a794-b114ab69aced" />

---

### 4. Regional Performance & Discount Distribution
* **Focus:** Geographic sales balance and regional pricing discipline.
* **Components:**
  * Regional Net Sales distribution:
    * **East:** $636.79K (30.09%)
    * **West:** $617.97K (29.20%)
    * **Central:** $487.23K (23.02%)
    * **South:** $374.41K (17.69%)
  * Profit generation disparity: West generates **73.19%** of all net profit, whereas Central produces only **8.26%**.
  * Total discount allocation: Central applied the highest accumulated discounts (**558.34**), directly explaining its depressed net profit yield.
  * <img width="3075" height="1763" alt="Mini Project 2 (Power BI) - Mourine_page-0004" src="https://github.com/user-attachments/assets/da1e9f8e-c5db-4b52-af0d-08aad1ef813e" />

---

### 5. Monthly Trends & Time Intelligence
* **Focus:** Macro-level trends over time and margin volatility.
* **Components:**
  * Monthly Net Sales and Net Profit trends.
  * Cumulative Running Total trajectory (reaching $657.71K).
  * Monthly Profit Margin variations (highest in **March at 4.49%**; lowest in **July at -2.07%** and **January at -0.91%**).
  * Profitability category distribution mapped across calendar months.
  * <img width="3075" height="1763" alt="Mini Project 2 (Power BI) - Mourine_page-0005" src="https://github.com/user-attachments/assets/b1ae292f-069f-439f-93e8-1a8b59c80fc6" />

---

## 🛠️ Data Modeling & DAX Measures

The data model uses a clean Star Schema design with dedicated fact tables for Sales and Returns, connected to dimension tables for Calendar, Geography, and Products.

Key calculated measures implemented include:

## ⚙️ Data Modeling & DAX Measures

The analytical foundation utilizes customized DAX measures to guarantee accurate business logic and revenue tracking:

```dax
// 1. Total Gross Sales
Total Sales = SUM(Orders[Sales])

// 2. Returned Sales Value
Returned Sales = 
CALCULATE(
    [Total Sales],
    FILTER(Orders, RELATED(Returns[Returned]) = "Yes")
)

// 3. True Net Sales (Adjusted for Returns)
Net Sales = [Total Sales] - [Returned Sales]

// 4. Total Gross Profit
Total Profit = SUM(Orders[Profit])

// 5. Net Profit (True Retained Profit)
Net Profit = 
VAR ReturnedProfit = 
    CALCULATE(
        [Total Profit], 
        FILTER(Orders, RELATED(Returns[Returned]) = "Yes")
    )
RETURN
    [Total Profit] - ReturnedProfit

// 6. Net Profit Margin Percentage
Profit Margin = DIVIDE([Net Profit], [Net Sales], 0)

// 7. Year-over-Year (YoY) Sales Growth
YOY Growth% = 
VAR PrevYearSales = CALCULATE([Net Sales], SAMEPERIODLASTYEAR('Calendar'[Date]))
RETURN
    DIVIDE([Net Sales] - PrevYearSales, PrevYearSales, 0)

// 8. Year-to-Date Running Total
Running Total = TOTALYTD([Net Sales], 'Calendar'[Date])
```

---

## 📊 Profitability Segmentation Logic

#### Overview
Rather than relying on arbitrary, static thresholds or manual pre-processing in Excel, the data model incorporates a dynamic statistical framework directly in DAX using the **Interquartile Range (IQR)** method.

#### Business Rationale
- **Investigation Alerts over "Outlier" Dismissal:** Extreme figures (e.g., negative margins reaching -300%) are categorized as alerts for targeted business investigation (e.g., pricing leakage, aggressive discounting, or high fulfillment costs) rather than being immediately discarded as noise.
- **Five Actionable Tiers:**
  1. `Severe Loss`: Margins falling below the lower statistical fence ($Q1 - 1.5 \times IQR$).
  2. `Loss`: Margins sitting between the lower fence and the 25th percentile ($Q1$).
  3. `Medium Profit`: Core baseline performance between $Q1$ and $Q3$.
  4. `High Profit`: Strong performers between $Q3$ and the upper fence.
  5. `Exceptional Profit`: Margins exceeding the upper fence ($Q3 + 1.5 \times IQR$) that may represent high-performing opportunities or pricing anomalies.
  <img width="514" height="203" alt="Profitability Category" src="https://github.com/user-attachments/assets/5a951186-c250-4cd7-8514-3196d7628b09" />

---

## 💡 Strategic Recommendations

1. Re-evaluate Discounting Thresholds in the Central Region:
   The Central region registered the highest discount values (558.34) but yielded only 8.26% of company profit. Strict discount caps should be introduced immediately to prevent value erosion.
2. Quality Control on High-Return Sub-Categories:
   Phones and Chairs contribute disproportionately to the $180.50K returned merchandise. An operational audit on packaging and delivery handling for these items is recommended.
3. Address Margin Losses in Furniture:
   While Furniture generates healthy gross sales ($0.67M), its margin stands at an alarming 0.5%, weighed down by heavy losses in Tables and Bookcases. Re-negotiate supplier pricing or adjust catalog pricing.

---

## 👤 Author & Contact

* Developer: Mourine Emad
* LinkedIn: https://www.linkedin.com/in/mourine-emad-ba2a301b5/
* GitHub: https://github.com/mourineemad/mourineemad
