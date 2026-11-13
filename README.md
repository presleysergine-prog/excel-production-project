# Excel Production Project: Production Performance Dashboard

This Excel Production project is an interactive dashboard that analyses a production dataset covering **120 production tasks**, **10 managers**, **4 product types** and **4 regions**, from **September 2023 to September 2024**.

Built with: **Microsoft Excel** (data cleaning, PivotTables, PivotCharts, Slicers, Timeline).

---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Business Questions](#2-business-questions)
3. [Dataset Description](#3-dataset-description)
4. [Data Cleaning and Preparation](#4-data-cleaning-and-preparation)
5. [Analysis Workbook Structure](#5-analysis-workbook-structure)
6. [Chart-by-Chart Analysis](#6-chart-by-chart-analysis)
7. [Key Insights and Findings](#7-key-insights-and-findings)
8. [Conclusion](#8-conclusion)
9. [Repository Structure](#11-repository-structure)

---

## 1. Project Overview

The goal of this project is to turn raw production records into a one page dashboard that helps management understand:

- Where production money is going (cost by product type)
- How output changes over time (units by year and month)
- How work is distributed across managers (number of tasks)
- How expensive each unit is to produce (average cost per unit)

---

## 2. Business Questions

1. Which product type consumes the most production cost?
2. Which product type is the most expensive to produce per unit?
3. How has production output moved month by month?
4. How evenly are tasks spread across managers?
5. Can the results be filtered by Region, Gender, Age Group and time period?

---

## 3. Dataset Description

Sheet: **Production Dataset**

| Column | Description |
|---|---|
| ProductionID | Unique ID of each production record (1 to 120) |
| ProductionDate | Date of production |
| Region | East, North, South, West |
| Manager | Manager responsible for the task (10 managers) |
| ProductType | Automobiles, Electronics, Furniture, Machinery |
| UnitsProduced | Number of units produced |
| TotalCost | Total production cost of the record |
| Gender | Female, Male, Unknown |
| New Age | Cleaned age value |
| Age Groups | **Derived column**: A1, A2, A3 |
| Production Cost Per Unit | **Derived column**: `TotalCost / UnitsProduced` |

Cleaned dataset

<img width="2558" height="1528" alt="cleaned" src="https://github.com/user-attachments/assets/155ed852-2593-4a49-abf2-0a6df7e4ea44" />

---

## 4. Data Cleaning and Preparation

All cleaning was done in Excel before building the PivotTables.

### 4.1 Missing values
- Checked every column for blanks (Home > Find & Select > Go To Special > Blanks, and filter dropdowns).
- Missing **Gender** values were labelled **"Unknown"** instead of being deleted, so the records (and their cost and units) stay in the analysis. This is why the Gender slicer shows Female, Male and Unknown.
- Missing / inconsistent ages were corrected into a cleaned column called **New Age**.

### 4.2 Duplicates
- Used **Data > Remove Duplicates** (also available on Table Design) on the full record to remove repeated rows.
- Confirmed that `ProductionID` is unique after the clean up (IDs run 1 to 120, matching the 120 tasks in the Number of Task pivot).

### 4.3 Data type and format fixes
- `ProductionDate` converted to proper Excel dates (used for Year / Month grouping and the Timeline slicer).
- Numeric columns (`UnitsProduced`, `TotalCost`) stored as numbers.
- Data converted to an Excel Table (`Table1`) so PivotTables refresh automatically.

### 4.4 Feature engineering
**Age Groups (new column).** Ages were bucketed into three groups. From the cleaned data the groups behave as follows:

| Age Group | Ages observed in the data |

<img width="2360" height="314" alt="Annotation 2026-11-13 051240" src="https://github.com/user-attachments/assets/fcaeb718-5f90-40ed-b978-7e304072d363" />

---

## 5. Analysis Workbook Structure

| Sheet | Purpose |
|---|---|
| Product Type Chart | Total cost by product type (PivotTable + column chart) |
| Number of Task | Task count by manager (PivotTable + bar chart) |
| Yearly and Monthly Trend | Units produced by year / month (PivotTable + line chart) |
| Average Production Cost | Average cost per unit by product type (PivotTable + pie chart) |
| Dashboard | All charts + slicers (Region, Gender, Age Groups, Quarters) + Timeline |
| Production Dataset | Cleaned source data |

Slicers on the dashboard: **Region** (East, North, South, West), **Gender** (Female, Male, Unknown), **Age Groups** (A1, A2, A3), **Quarters** (Qtr1 to Qtr4) and a **date Timeline**. They are connected to all PivotTables so every chart updates together.

---

## 6. Chart by Chart Analysis

### 6.1 Total production cost by product type
<img width="2560" height="1528" alt="Annotation 2026-11-11 133937" src="https://github.com/user-attachments/assets/6bb42a2f-8b5b-4a7c-89d0-55949dae3cda" />

- Automobiles alone cost about **1.9x** as much as Electronics.
- Automobiles + Machinery account for **over 61%** of all production cost.

### 6.2 Number of Tasks by Manager
<img width="2560" height="1519" alt="Annotation 2026-11-12 065618" src="https://github.com/user-attachments/assets/45b48110-4f58-4bfa-b1d8-eda91d7bc149" />

- Nancy Grey handles **almost one in three tasks** and is roughly **7x** Sarah Lee's workload.
- The top 3 managers (Nancy Grey, Jane Smith, John Doe) handle **68 of 120 tasks (56.7%)**.
- The bottom 4 managers handle only 23 tasks (about 19%) combined.

### 6.3 Total Units Produced by Year / Month
<img width="2556" height="1526" alt="Annotation 2026-11-12 070936" src="https://github.com/user-attachments/assets/e87b99c3-4456-41ad-9439-592efe505075" />

- Highest month: **Nov 2023 (4,803)**. Second highest: **Feb 2024 (4,127)**.
- Lowest months: **Sep 2023 (771)** and **Sep 2024 (1,379)**; both are likely **partial months** (the timeline slicer shows the data starting around 22 Sep 2023 and ending around 15 Sep 2024).
- Output **fell sharply after March 2024**: from 3,875 units in March to 1,528 in April (about -61%).
- Output is **volatile**, alternating between peaks (Feb, Jun, Aug) and dips (Apr, May, Jul, Sep).

### 6.4 Average Production Cost per Unit by Product Type
<img width="2560" height="1523" alt="Annotation 2026-11-12 072647" src="https://github.com/user-attachments/assets/19a52e59-2ea7-4e72-bed4-572317473b89" />

- **Furniture is the most expensive product per unit** (about 66% more than Electronics).
- Machinery and Electronics have almost identical unit costs (about 108 to 109).
- Interesting contrast: Furniture is only 3rd in *total* cost, but 1st in *cost per unit*; Automobiles are 1st in total cost because of volume and a high unit cost.

### 6.5 Final Dashboard
<img width="2179" height="1182" alt="dashboard" src="https://github.com/user-attachments/assets/2ed56ad9-f6d5-4c7a-bcd2-f26a5f6c6c72" />

All four charts are placed on one page with a dark blue header ("PRODUCTION DASHBOARD"), a logo, and slicers on the left for Region, Gender, Age Groups, Quarters and a date Timeline.

---

## 7. Key Insights and Findings

**Cost**
1. Total production cost is **3,371,078** across all product types.
2. **Automobiles (34.2%)** and **Machinery (27.0%)** drive over 61% of the cost; **Electronics is the cheapest line (17.9%)**.

**Unit economics**

3. **Furniture has the highest average cost per unit (180.44)**, well above the overall average of 132.39.
4. Electronics and Machinery are the most cost-efficient per unit (about 108 to 109).
5. Overall, the dataset produced **34,727 units** for **3,371,078** total cost. That gives a **weighted cost per unit of about 97.07** (total cost / total units), which is noticeably **lower than the 132.39 simple average** shown in the pivot. The simple average is pulled up by a few records with very low units and high cost (for example ProductionID 9: 55 units, cost per unit 471; ProductionID 23: 90 units, cost per unit 470).

**Workload**

6. Task distribution is **highly uneven**: Nancy Grey has 37 of 120 tasks (30.8%).
7. Five managers each handle 6 tasks or fewer, so capacity is likely under-used.

**Time trend**

8. Production peaked in **Nov 2023** and again in **Feb to Mar 2024**.
9. A **steep drop occurred in Apr 2024**, and output has not returned to the early-2024 level; Q3 2024 (5,779 units) is about **48% below** Q1 2024 (11,028 units).
10. Recurring spikes (Nov, Feb, Jun, Aug) suggest **seasonal or order-driven production**.

---

## 8. Conclusion

The production operation is **cost concentrated, workload concentrated and volatile in output**.

- **Automobiles and Machinery** are the main cost centres, while **Furniture** is the least efficient product per unit.
- **Nancy Grey** carries a disproportionate share of the work, which is a potential bottleneck and key person risk.
- Output was strongest from **Nov 2023 to Mar 2024** and declined and became unstable afterwards, with Q3 2024 being roughly half of Q1 2024.
- The cleaned dataset (missing values handled, duplicates removed, Age Groups created) and interactive slicers make it easy to drill down by region, gender, age group and period.
- 
---

## 11. Repository Structure

```
excel-production-project/
│
├── README.md
├── Production_Excel_Dashboard.xlsx      
├── images/
│   ├── 01_total_cost_by_product_type.png    
│   ├── 02_number_of_tasks_by_manager.png    
│   ├── 03_units_by_year_month.png           
│   ├── 04_avg_cost_per_unit_pie.png         
│   ├── 05_dashboard.png                    
│   └── 06_cleaned_dataset.png               
└── data/
    └── Production_Dataset.xlsx               

```

---

## 👤 Author

**Presley Ufuoma Sergine**
Data Analyst | Lagos, Nigeria

[LinkedIn](https://www.linkedin.com/in/your-profile) | [Email](mailto:presleysergine23@gmail.com)
