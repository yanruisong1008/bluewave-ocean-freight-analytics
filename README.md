# BlueWave Logistics: Trans-Pacific Ocean Freight Performance Analytics

> An end-to-end Power BI project analyzing carrier reliability, transit performance, freight cost and customer volume for a (fictional) freight forwarder shipping from Asia to the United States.

![Report overview](images/00_overview.png)
<!-- TODO (M4): replace with a screenshot or GIF of the finished report -->

## Business Context

BlueWave Logistics is a mid-sized freight forwarder moving full-container-load (FCL) shipments from seven Asian origin ports to eight US gateway ports. Operations, procurement and sales teams each pull their own spreadsheets, so nobody shares one view of how carriers are performing or where margin is being lost.

This project builds a single Power BI report that answers the questions those teams ask every week.

## Business Questions

1. **Reliability**: Which carriers and lanes deliver on time, and how has schedule reliability changed month to month?
2. **Delays**: Where do delays happen, how long are they, and what causes them?
3. **Cost & Margin**: How are freight costs moving, what does a TEU cost on each lane, and which customers and lanes earn the best margin?
4. **Volume**: Who are the largest customers by TEU, and how does actual volume compare with the 2026 budget?
5. **Billing Cycle**: How many days pass from door delivery to invoice submission (policy: 30 days) and from invoice submission to payment (policy: 45 days)? Which customers and months break policy, and did the 2026 billing process improvement work?

<!-- TODO (M1): refine these questions and add 1–2 of your own from real operations experience -->

## Data

All data is **synthetic**, generated with [`scripts/generate_data.py`](scripts/generate_data.py). Company, carrier and customer names are fictional; port codes are real UN/LOCODEs.

| Source | Format | Content |
|---|---|---|
| `data/raw/shipments/` | 21 monthly CSV files | ~2,900 shipments, Jan 2025 – Sep 2026 |
| `data/raw/master_data.xlsx` | Excel, 4 sheets | Carriers, ports, customers, container types |
| `data/raw/budget_2026.xlsx` | Excel, wide format | 2026 monthly TEU and revenue budget by destination region |
| `data/raw/invoices.csv` | CSV (billing system export) | ~2,800 customer invoices: door delivery, invoice submitted, invoice paid |

The raw files deliberately contain real-world data quality problems (inconsistent carrier names, mixed date locales, duplicates, text-formatted numbers, report-style headers). See [`docs/DATA_DICTIONARY.md`](docs/DATA_DICTIONARY.md).

## Excel Prototype (M0)

<!-- TODO (M0): screenshot of the Excel executive summary (excel/BlueWave_Executive_Summary.xlsx) and 2–3 sentences on what was calculated (margin, transit/delay days, delay category). Contrast the manual Excel cleanup with the automated Power Query pipeline below. -->

## Data Preparation (Power Query)

<!-- TODO (M2): describe the transformation steps and add a screenshot of the query dependencies view -->

## Data Model

<!-- TODO (M3): add model diagram screenshot (images/01_data_model.png) and explain the star schema -->

## Key DAX Measures

<!-- TODO (M3): list 5–8 measures with a one-line purpose each, e.g. On-Time %, Avg Delay Days, Cost per TEU, Budget Variance %, Avg Days to Invoice, Avg Days to Pay, % Invoices Over Policy -->

| Measure | Purpose |
|---|---|
| | |

## Report Pages

<!-- TODO (M4/M5): one screenshot + 2–3 sentences per page -->

## Key Insights

<!-- TODO (M4): 3–5 findings written as a business recommendation, not a chart description -->

## Security & Deployment

<!-- TODO (M6): row-level security by sales region, publishing, refresh -->

## Skills Demonstrated

<!-- TODO: fill in as each milestone is completed -->

## Repository Structure

```
├── data/raw/              source files (CSV + Excel)
├── docs/                  data dictionary and notes
├── excel/                 Excel prototype and executive summary
├── images/                report screenshots used in this README
├── report/                Power BI file (.pbix)
└── scripts/               Python data generator
```

## How to Open

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Windows).
2. Download or clone this repository.
3. Open `report/BlueWave_Ocean_Freight.pbix`. If prompted, point the data source paths to your local `data/raw/` folder.

---

*Author: Aria (Yanrui Song) · [LinkedIn](#) <!-- TODO: add link -->*
