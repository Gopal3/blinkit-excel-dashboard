# Blinkit Grocery Sales — Excel Dashboard (Reproducible Project)

A reproducible Excel analytics project analyzing Blinkit grocery sales data — fully rebuilt from scratch and documented step by step.

This repository contains an **Excel-based analytics dashboard** I rebuilt and extended using a public dataset and a tutorial as a reference point.  
My goal was to turn a one-off tutorial file into a **documented, reproducible, and improvable project** that reflects my own workflow and decisions.

> **Attribution:** This project was inspired by a YouTube tutorial. Full credit to the original author for the initial concept and dataset reference.  
> I rebuilt the workbook from scratch, applied my own transformations, and documented the entire process to clearly separate my work from the tutorial.

---

## 🔎 Project Overview

- **Tooling:** Microsoft Excel (recommended: Microsoft 365 or Excel 2019+) — no add-ins required  
- **File:** `Blinkit_Analysis_Dashboard.xlsx`  
- **Data sheet:** `BlinkIT Grocery Data` (8,523 rows × 13 columns)  
- **Purpose:** Analyze sales patterns across item types, outlet types, sizes, locations, and other attributes; publish a clean, versioned Excel analytics project

### Key KPIs (from the current workbook)
- Total Sales (sum): **1,201,681.49**  
- Average Sales per row: **140.99**  
- Average Rating: **3.97 / 5**  
- Unique Items: **1,559**  
- Unique Outlets: **10**  
- Establishment Years: **2011–2022**  
- Missing values noted in `Item Weight`: **1,463**

> Exact numbers will recompute from the workbook; these are provided for reference.

---

## 🧱 Repository Structure

```
.
├── Blinkit Analysis Dashboard (Excel).xlsx   # Main Excel file
├── README.md                                 # This file
└── /docs
    └── change_log.md                         # What I changed vs tutorial
    
```

## ✅ What I Did (End-to-End)

### 1️⃣ Understand the Raw Data
- Opened the `BlinkIT Grocery Data` sheet and reviewed the schema:
  - Columns include: `Item Identifier`, `Item Type`, `Item Fat Content`, `Item Weight`, `Item Visibility`, `Total Sales`, `Outlet Type`, `Outlet Location Type`, `Outlet Size`, `Outlet Establishment Year`, `Rating`, etc.
- Ran quick checks:
  - Identified missingness (`Item Weight` has ~1.7k nulls)
  - Spotted inconsistent categories in `Item Fat Content` (`LF`, `low fat`, `Low Fat`), and in `Outlet Size` / `Outlet Location Type`

### 2️⃣ Clean & Standardize
- **Category Standardization**
  - Re-mapped `Item Fat Content` → `Low Fat`, `Regular`, `Other`
  - Normalized `Outlet Size` (Small, Medium, High) and `Outlet Location Type` (Tier 1/2/3)
- **Missing Values**
  - Imputed `Item Weight` via **median by Item Type** (robust against outliers)
- **Derived Fields**
  - `Outlet Age` = **2025 − Outlet Establishment Year**
  - `Sales per Kg` = **Total Sales / Item Weight** (after imputation)
  - `Visibility Bins` = binned ranges of `Item Visibility` for segment analysis

> All transformations are documented in-workbook (notes area in `Sheet Design`) for transparency.

### 3️⃣ Build the Model (Pivots & Measures)
- Created **PivotTables** to summarize:
  - Sales by `Item Type`, `Outlet Type`, `Location Type`, and `Outlet Size`
  - Average `Rating` and `Sales per Kg` by the same dimensions
  - Sales vs `Visibility Bins` (shelf-visibility effect)
- Added calculated fields where useful for ratios and contribution analysis

### 4️⃣ Design the Dashboard (`DashBoard` sheet)
- **Layout:** Header with KPIs → filters → visual grid  
- **KPIs:** Total Sales, Avg Sales, Avg Rating, Unique Items, Unique Outlets, Median Outlet Age  
- **Visuals:** Clustered bar (Item Type sales), stacked bar (Outlet Type × Location), donut (Fat Content mix), line (Sales by Year), and heatmap for Sales vs Rating  
- **Interactivity:** Slicers for `Item Type`, `Outlet Type`, `Outlet Location Type`, `Outlet Size`, `Item Fat Content`, and `Visibility Bins`  
- **Usability:** Consistent number formats, compact labels, minimalist design

### 5️⃣ QA & Sanity Checks
- Verified totals between PivotTables and KPI cards  
- Tested slicers for edge cases and blank filters  
- Spot-checked data points between raw and pivot outputs  
- Ensured the imputed `Item Weight` distribution looked reasonable  
- Documented key assumptions and limitations

---

## 🆚 How This Differs from the Tutorial

💡 **My Key Contributions**
- Rebuilt the entire dashboard manually from a blank Excel workbook  
- Standardized messy data categories (Item Fat Content, Outlet Size)  
- Added new KPIs: **Sales per Kg**, **Outlet Age**, and **Visibility Bins**  
- Introduced cleaner visual design and slicer usability improvements  
- Documented everything in this README and a versioned changelog  
- Added structured QA checks for consistent KPI calculations  

---

## 🙌 Attribution

I respect the original tutorial creator and the effort that inspired this work.  
This repository demonstrates my ability to **extend and professionalize** a learning project into a reproducible, documented analytics workflow.

---

## 📜 License

Licensed under the [MIT License](LICENSE).

Use any OSI-approved license that fits your goals. If unsure, MIT is a safe default for showcasing.
