# Real Estate Analytics Dashboard | Power BI

An interactive Power BI dashboard that analyzes real estate market performance across U.S. cities — tracking listing prices, agent productivity, property distribution, and month-over-month market trends.

![Dashboard Preview](images/dashboard-preview.png)

---

## 📌 Project Overview

This dashboard provides a 360° view of a real estate business — designed for executives, sales managers, and agents to quickly understand market health and identify opportunities. It transforms raw transactional data into actionable insights through dynamic KPIs, geographic visualization, and agent performance metrics.

**Built with:** Microsoft Power BI Desktop
**Data modeling:** DAX, Star Schema
**Visuals:** New Card Visual, Donut, Bar, Map, Slicers, Tables

---

## 🎯 Business Questions Answered

- What is the current average list price, and how does it compare to last month?
- How many active listings are in the market right now?
- Which cities are driving the highest property prices?
- How is the property portfolio distributed across types (Residential / Rental) and statuses (Active / Sold / Pending)?
- Which agents are performing best in terms of properties handled, commission, and close rates?
- Where are properties geographically concentrated?

---

## 📊 Key Features

### 1. KPI Cards with MoM Trend Indicators
- **Average List Price** with arrow indicator showing month-over-month change
- **Active Listings** count with growth percentage vs. previous month
- Built using DAX with `DATEADD` and dynamic text formatting

### 2. Agent Performance Tracking
- **Avg Properties per Agent** — productivity metric
- **Avg Commission %** — revenue efficiency
- **Close Rate %** — conversion performance

### 3. Geographic & Categorical Analysis
- City-wise average list price ranking
- Property distribution by type (Residential vs. Rental)
- Status distribution (Active / Sold / Pending)
- Interactive map showing property concentration by city

### 4. Detailed Property Listings Table
Drillable property-level data with PropertyID, City, State, Type, prices, agent name, and days on market.

### 5. Dynamic Filtering
- Month and Year slicers for time-based analysis
- All visuals respond to slicer selections

---

## 🛠️ Tech Stack

| Component | Tool / Technique |
|-----------|------------------|
| Data Source | CSV (`real_estate.csv`) |
| ETL | Power Query Editor |
| Data Modeling | Star Schema with Date dimension table |
| Calculations | DAX measures |
| Visualization | Power BI Desktop |
| Version Control | Git / GitHub |

---

## 🗂️ Data Model

The model uses a **star schema** with a dedicated Date dimension table for time intelligence calculations.

![Data Model](images/data-model.png)

**Tables:**
- `real_estate` (fact table) — property listings, agent info, pricing, dates
- `Date` (dimension) — calendar table with MonthName, YEAR, YearMonth
- `_Measures` (measures-only container)

**Relationship:** `real_estate[ListingDate]` → `Date[Date]` (Many-to-One)

---

## 🧮 Key DAX Measures

**Average List Price**
```DAX
AvgListPrice = AVERAGE(real_estate[ListPrice])
```

**Month-over-Month Growth %**
```DAX
ActiveListingPrice_MoM_Growth % =
VAR _CurrentMonth = [AvgListPrice]
VAR _LastMonth =
    CALCULATE([AvgListPrice], DATEADD('Date'[Date], -1, MONTH))
RETURN
    DIVIDE(_CurrentMonth - _LastMonth, _LastMonth, 0)
```

**MoM Display (with arrow indicator)**
```DAX
ActiveListingPrice_MoM_Display =
VAR _VarPct = [ActiveListingPrice_MoM_Growth %]
RETURN
    IF(_VarPct > 0, "↗", "↘")
    & " "
    & FORMAT(_VarPct, "0%")
    & " vs last month"
```

Full DAX reference: [`docs/dax-measures.md`](docs/dax-measures.md)

---

## 🚀 How to Use

1. Clone or download this repository.
2. Open `Real_Estate_Report.pbix` in **Power BI Desktop** (version 2.140 or later recommended).
3. If prompted, refresh the data source path to point to `dataset/real_estate.csv`.
4. Interact with slicers (MonthName, YEAR) to filter the analysis.

---

## 📸 Dashboard Sections

### Overview KPIs

### Property & Agent Analysis
*Donut charts for distribution + agent performance cards*

### Geographic Distribution
*Bubble map showing city-level property concentration*

---

## 💡 Insights Discovered

- Philadelphia, Washington DC, and San Antonio lead in average list price
- Residential properties dominate the portfolio (~58% share)
- Close rate sits at ~38%, indicating room for sales process optimization
- Average commission percentage holds steady around 3.83%

---

## 🔄 Future Enhancements

- Add a "Last Refreshed" timestamp using `NOW()`
- Implement YoY (Year-over-Year) comparison alongside MoM
- Add agent-level drill-through pages
- Forecast next 3 months of price trends using built-in analytics
- Conditional formatting on the property table (color-code by status)

---


## 🙋 About Me

**DEVIKA SHAH**
Data Analyst | Power BI Developer
📍 Maharashtra, India

- 🔗 LinkedIn: linkedin.com/in/devikashah-data-analyst
- 📧 Email: devikashah2000@gmail.com


---

## 📜 License

This project is available for learning and portfolio purposes. Dataset is fictional / publicly available for educational use.

---

⭐ **If you found this project helpful, please star the repository!**
