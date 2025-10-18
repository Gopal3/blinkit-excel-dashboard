
# Blinkit Grocery Sales — Excel Dashboard (Reproducible Project)

This repository contains an **Excel-based analytics dashboard** I rebuilt and extended using a public dataset and a tutorial as a starting point. My goal was to turn a one-off tutorial file into a **documented, reproducible, and improvable project** that reflects my own workflow and decisions.

> **Important attribution:** This project was inspired by a YouTube tutorial. Full credit to the original author for the initial concept and dataset link. I rebuilt the workbook from scratch, made several design and analytical changes, and documented every step below to clearly separate my work from the tutorial.

---

## 🔎 Project Overview

- **Tooling:** Microsoft Excel (recommended: Microsoft 365 or Excel 2019+) — no add‑ins required.
- **File:** `Blinkit Analysis Dashboard (Excel).xlsx`
- **Data sheet:** `BlinkIT Grocery Data` (8,523 rows × 13 columns)
- **Purpose:** Understand sales patterns across item types, outlet types, sizes, locations, and other attributes; publish a clean, versioned Excel analytics project.

### Key KPIs (from the current workbook)
- Total Sales (sum): **1,201,681.49**
- Average Sales per row: **140.99**
- Average Rating: **3.97 / 5**
- Unique Items: **1,559**
- Unique Outlets: **10**
- Establishment Years: **2011–2022**
- Missing values noted in `Item Weight`: **1,463**

> Exact numbers will recompute from the workbook; they are documented here for quick reference.

---

## 🧱 Repository Structure

```
.
├── Blinkit Analysis Dashboard (Excel).xlsx   # Main Excel file
├── README.md                                 # This file
└── /docs
    └── change_log.md                         # What I changed vs tutorial
```

Consider adding later:
- `/img`: screenshots/gifs of the dashboard
- `/data`: raw or intermediate CSVs if you export any transformations
- `/scripts`: optional helper scripts (e.g., Python for QA checks)

---

## ✅ What I Did (End-to-End)

### 1) Understand the raw data
- Opened `BlinkIT Grocery Data` sheet and reviewed schema:
  - Columns include: `Item Identifier`, `Item Type`, `Item Fat Content`, `Item Weight`, `Item Visibility`, `Total Sales`, `Outlet Type`, `Outlet Location Type`, `Outlet Size`, `Outlet Establishment Year`, `Rating`, etc.
- Ran quick checks:
  - Looked for missingness (`Item Weight` has ~1.7k nulls).
  - Scanned for inconsistent categories in `Item Fat Content` (e.g., `LF`, `low fat`, `Low Fat`), and in `Outlet Size` / `Location Type`.

### 2) Clean & standardize
- **Category standardization**
  - Re-mapped `Item Fat Content` to consistent labels: `Low Fat`, `Regular`, `Other`.
  - Normalized `Outlet Size` (e.g., `Small`, `Medium`, `High`) and `Outlet Location Type` (e.g., `Tier 1/2/3`) where needed.
- **Missing values**
  - `Item Weight`: imputed via **median by Item Type** (more robust than global mean).
- **Derived fields**
  - `Outlet Age` = `CurrentYear` − `Outlet Establishment Year` (document the `CurrentYear` used; I use 2025 for reproducibility).
  - `Sales per Kg` = `Total Sales` / `Item Weight` (post‑imputation).
  - `Visibility Bins` = bins of `Item Visibility` for segment analysis.

> All transformations are **documented in‑workbook** on a notes area in `Sheet Design` for transparency.

### 3) Build the model (pivots & measures)
- Created **PivotTables** to summarize key relationships:
  - Sales by `Item Type` / `Outlet Type` / `Location Type` / `Outlet Size`.
  - Average `Rating` and `Sales per Kg` by the same dimensions.
  - Sales vs `Visibility Bins` (to explore shelf‑visibility effect).
- Added calculated fields inside pivots (where appropriate) for ratios and contributions.

### 4) Design the dashboard (`Dashboard` sheet)
- **Layout:** Header with KPIs → filters → main visual grid.
- **KPIs:** Total Sales, Avg Sales, Avg Rating, Unique Items, Unique Outlets, Outlet Age (median).
- **Visuals:** Clustered bar for Item Type sales, stacked bar for Outlet Type × Location, donut for Fat Content mix, line for sales by Establishment Year, heat/conditional format for Sales vs Rating.
- **Interactivity:** Slicers for `Item Type`, `Outlet Type`, `Outlet Location Type`, `Outlet Size`, `Item Fat Content`, and `Visibility Bins`. A **Reset Filters** button wired to clear slicers (macro‑free via Clear Filter icons or macro if desired).
- **Usability:** Labels, number formats, thousands separators, and data labels only when needed to avoid clutter.

### 5) QA & sanity checks
- Tied totals between all pivot elements and KPI cards.
- Stress‑tested slicers for contradictory filters and blank states.
- Spot‑checked a few items across raw data vs pivot totals.
- Documented assumptions and limits (e.g., imputation method).

---

## 🆚 How This Differs From the Tutorial

## 💡 My Key Contributions

- Rebuilt the entire dashboard manually from a blank Excel workbook.
- Standardized messy data categories (like Item Fat Content and Outlet Size).
- Created new KPIs: **Sales per Kg**, **Outlet Age**, and **Visibility Bins**.
- Added slicers and consistent formatting for cleaner visuals.
- Wrote detailed documentation (this README and a changelog).
- Performed QA checks to ensure correct pivot totals and clean interactivity.

---

## 🤝 Attribution

I respect content creators. This repo exists to demonstrate my **own workflow** and the **ability to extend** a tutorial into production‑style, documented work.

---

## 📜 License

Use any OSI-approved license that fits your goals. If unsure, MIT is a safe default for showcasing.
