# 💳 Credit Card Financial Dashboard | Power BI

An end-to-end business intelligence project that turns raw SQL transaction & customer data into a real-time, decision-ready dashboard for a credit card business — covering **56.5M in revenue**, **667K+ transactions**, and **10K+ customers**.

---

## 📌 Problem Statement

Credit card businesses generate massive volumes of weekly transaction and customer data — but raw data sitting in a database doesn't help stakeholders make decisions. Leadership needs a **single source of truth** to answer questions like:
- Is revenue trending up or down week-over-week?
- Which customer segments (age, income, job, education) drive the most revenue?
- Which card category and transaction channel (swipe/chip/online) is performing best?
- Where are activation and delinquency rates heading?

This project builds a **3-page interactive Power BI dashboard**, backed by a SQL database, to answer exactly that — refreshed on a **weekly cadence**.

---

## 🛠️ Tech Stack & Workflow

`CSV Data → SQL (PostgreSQL) → Power BI (Data Modeling + DAX) → Interactive Dashboard`

| Stage | Tool | What was done |
|---|---|---|
| Data Storage | **SQL (PostgreSQL)** | Created tables, imported 10K+ customer & transaction records via `COPY` |
| Data Modeling | **Power BI / DAX** | Built calculated columns & measures (age groups, income groups, week numbers, WoW revenue) |
| Visualization | **Power BI** | Built 3 linked report pages with cross-filtering slicers |
| Analysis | **DAX + Business Logic** | Derived KPIs: Activation Rate, Delinquency Rate, WoW % change |

---

## 📊 Dashboard Overview

### 1️⃣ Customer Report
Segments revenue and income by demographics — age group, gender, marital status, education, income group, dependent count, and job type — plus a Top 5 state breakdown.

### 2️⃣ Transaction Report
Breaks down revenue and transaction volume by card category, quarter, expenditure type (bills, fuel, grocery, travel, etc.), and channel used (swipe, chip, online).

### 3️⃣ Weekly Executive Summary
A KPI-first view built for leadership — current vs. previous week revenue, WoW % change, and headline YTD metrics — refreshed via a `week_start_date` slicer.

---

## 💡 Key Business Insights

- **Revenue grew 28.8% week-over-week** in the latest reporting week (Week 53)
- YTD **total revenue: ₹56.5M**, with **₹8M in interest** and **₹45.5M in transaction volume**
- **Male customers contributed ₹31M** in revenue vs. **₹26M from female customers**
- **Blue & Silver cards drive 93%** of all transactions — a strong signal for where retention efforts should focus
- **TX, NY & CA together contribute 68%** of total revenue — a clear geographic concentration
- **Swipe transactions (₹36M) dominate** over chip (₹17M) and online (₹4M) — relevant for fraud/security prioritization
- Overall **activation rate: 57.5%**, **delinquency rate: 6.06%** — both tracked as core risk KPIs

> These insights were used to simulate a real stakeholder review — the kind of storytelling an analyst is expected to deliver, not just a chart dump.

---

## 🧮 Sample DAX Measures

```DAX
Revenue = 
'cc_detail'[annual_fees] + 'cc_detail'[total_trans_amt] + 'cc_detail'[interest_earned]

Current_Week_Revenue = 
CALCULATE(
    SUM('cc_detail'[Revenue]),
    FILTER(ALL('cc_detail'), 'cc_detail'[week_num2] = MAX('cc_detail'[week_num2]))
)

AgeGroup = 
SWITCH(
    TRUE(),
    'cust_detail'[customer_age] < 30, "20-30",
    'cust_detail'[customer_age] < 40, "30-40",
    'cust_detail'[customer_age] < 50, "40-50",
    'cust_detail'[customer_age] < 60, "50-60",
    "60+"
)
```
Full SQL scripts and DAX queries are available in this repo under `/sql` and `/dax`.

---

## 📁 Repo Structure

```
├── data/                # Raw CSV files
├── sql/                 # Table creation + import scripts
├── dax/                 # DAX measures & calculated columns
├── Credit_Card_Dashboard.pbix
├── screenshots/         # Dashboard preview images
└── README.md
```

---

## 🚀 What I Learned

- Structuring a data model that supports **week-over-week trend analysis**, not just static totals
- Writing **DAX time-intelligence logic** (current vs. previous period comparisons) from scratch
- Translating raw metrics into **stakeholder-ready insights**, not just visuals
- Designing a dashboard with **real UX thinking** — slicers, KPI cards, and drill-downs that mirror how a business analyst would actually be asked to present this

---

## 🔗 Connect

If you have feedback or questions about this project, feel free to reach out.

**LinkedIn:** https://www.linkedin.com/in/prince-maurya-5a493227b
