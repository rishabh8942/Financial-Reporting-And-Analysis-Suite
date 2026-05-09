# 📊 Financial Reporting & Analysis — Power BI Dashboard

> An interactive financial reporting suite built in Power BI, delivering P&L performance, gross profit, net profit, EBITDA, and cross-country revenue analysis — designed for CFO and executive consumption.

---

## 🧭 Project Overview

This Power BI project transforms raw General Ledger data into a structured, drill-through financial reporting suite. Using a clean star-schema data model and DAX measures, it surfaces the key P&L metrics finance teams and leadership need — without manual Excel reconciliation.

The dashboard is built around a **Chart of Accounts hierarchy** (Class → SubClass → SubClass2 → Account), enabling meaningful drill-down from high-level financial summaries all the way to individual account lines.

---

## 🖼️ Report Pages

| Page | Description |
|------|-------------|
| **Sales** | Sales revenue trend analysis — pivot table + dual line charts with time-series drill-down (Year → Quarter → Month → Day) |
| **P&L** | Full Profit & Loss view — Sales Revenue, Gross Profit, Operating Profit, EBITDA, PBIT, and Net Profit with KPI cards and trend lines |
| **CrossCountry** | Country-level comparison of Sales Revenue, Gross Profit, and Net Profit filtered by territory |
| **P&L (Extended)** | Enhanced P&L page with combo charts — Sales vs Marketing Cost overlay, Gross Profit Margin %, and Net Profit Margin % pivot tables |

---

## 🗄️ Data Model

The report uses a **star schema** with four core tables:

```
tbl_GL (Fact)
├── Amount              ← Raw transaction amounts
├── SalesFTP            ← Sales figure (forecast/actual)
├── GrossProfit         ← Calculated gross profit
├── NetProfit           ← Calculated net profit
├── GPMargin            ← Gross profit margin %
├── NPMargin            ← Net profit margin %
├── MarketingCostFTP    ← Marketing cost
└── Total_FTP           ← Total aggregated financial figure

tbl_ChartofAccounts (Dimension)
├── Class               ← Top-level: Trading account | Expenses | Profit and Loss
├── SubClass            ← Mid-level grouping
├── SubClass2           ← Secondary sub-grouping
└── Account             ← Individual GL account line

tbl_Calendar (Date Dimension)
├── Date                ← Date key
└── Year                ← Year (with hierarchy: Year > Quarter > Month > Day)

tbl_territory (Dimension)
└── Country             ← Country filter for cross-country analysis
```

---

## 📐 Measures & Calculations

| Measure | Description |
|---------|-------------|
| `Total_FTP` | Core aggregated financial measure used across all P&L line items |
| `SalesFTP` | Sales revenue — forecast/actual period total |
| `GrossProfit` | Revenue minus cost of goods sold |
| `NetProfit` | Bottom-line profit after all deductions |
| `GPMargin` | Gross profit as a % of sales revenue |
| `NPMargin` | Net profit as a % of sales revenue |
| `MarketingCostFTP` | Total marketing expenditure for the period |
| `Sum(Amount)` | Raw GL amount aggregation for base-level analysis |

---

## 📊 Visuals Used

| Visual Type | Page | Usage |
|-------------|------|-------|
| **Matrix (Pivot Table)** | Sales, P&L | P&L breakdown by Chart of Accounts rows × Date Hierarchy columns |
| **Line Chart** | Sales, P&L, CrossCountry | Revenue, Gross Profit, Net Profit trends over time |
| **Line & Clustered Column Combo** | P&L Extended | Sales Revenue vs Marketing Cost overlay |
| **Line & Stacked Column Combo** | P&L Extended | Sales-to-Marketing cost ratio analysis |
| **Card** | P&L | Sales Revenue TTD (To-Date) headline KPI |
| **KPI Visual** | P&L | Sales FTP — target vs actual with trend indicator |
| **Slicer** | P&L, CrossCountry | Country filter from `tbl_territory`, synced across pages |

---

## 🔍 Drill-Down Structure

All time-based visuals support full **Date Hierarchy** drill-down:

```
Year  →  Quarter  →  Month  →  Day
```

The P&L matrix supports row-level drill-down via the **Chart of Accounts** hierarchy:

```
Class  →  SubClass  →  SubClass2  →  Account
```

**Chart of Accounts classes included:**
- `Trading account` — Revenue and direct cost lines
- `Expenses` — Operating expense categories
- `Profit and Loss` — Summary lines (Gross Profit, EBITDA, PBIT, Net Profit)

---

## 🚀 Getting Started

### Prerequisites
- Power BI Desktop (February 2024 or later)
- Source GL data matching the schema below
- *(Optional)* Power BI Pro for publishing and scheduled refresh

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/rishabh8942/financial-reporting-powerbi.git
   ```

2. **Open the report**  
   Launch Power BI Desktop → Open `report/Financial_Reporting_And_Analysis.pbix`

3. **Connect your data**  
   Go to **Transform Data → Data Source Settings** and point the source to your GL data file.  
   Your source data should include:

   | Column | Description |
   |--------|-------------|
   | `Date` | Transaction date |
   | `Amount` | Transaction amount |
   | `Account` | GL account code/name |
   | `Class` | Account class (Trading account / Expenses / P&L) |
   | `SubClass` | Account sub-grouping |
   | `Country` | Territory/country |

4. **Refresh the data**  
   Click **Refresh** in the Home ribbon and verify all tables load without errors.

5. **Publish** *(optional)*  
   Click **Publish** → select your workspace → configure scheduled refresh via Gateway.

---

## 💡 How to Use

- **Country Slicer** — Filter all visuals by territory on the P&L and CrossCountry pages
- **Date drill-down** — Click the ↓ arrow on any chart to go Year → Quarter → Month → Day
- **Account drill-down** — Expand Class rows in the P&L matrix to reach SubClass and individual Accounts
- **KPI Visual** — Check Sales FTP vs target at a glance with trend direction indicator
- **CrossCountry page** — Side-by-side Revenue, Gross Profit, Net Profit comparison across markets
- **P&L Extended** — Compare Sales vs Marketing spend and track margin % trends over time

---

## 🛠️ Tech Stack

| Tool | Role |
|------|------|
| **Power BI Desktop** | Report authoring, data modeling, publishing |
| **DAX** | Margin calculations, KPI measures, aggregations |
| **Power Query (M)** | ETL — data shaping and transformation |
| **Star Schema** | `tbl_GL` fact + 3 dimension tables |
| **Excel** | Upstream data source for GL and budget data |

---

*Built to replace static Excel P&L reports with a self-serve, interactive financial reporting layer — from top-line Sales Revenue down to individual GL account lines, filterable by country and drillable by time period.*
