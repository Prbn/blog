
---

### 🔹 **Organizational Structure & Allocation Context**
- Different business units (LOBs like Commercial and Consumer) receive **allocated expenses** from centralized services.
- **CIU group** (technology, task platforms) allocates costs to other business units (LOBs).
- Allocation is tracked by specific **products**:
  - **Consumer products**: Home equity, Mortgage, Credit cards (e.g., RCS card)
  - **Commercial products**: Lower section in product list

---

### 🔹 **Expense Reporting & Views**
- **Monthly Allocation Reports**: Aimed to track actual allocations per business unit.
- **Reports allow drill-down**:
  - From high-level LOBs to specific functional areas (e.g., Wealth → Direct channel → Residential Lending)
- **Product Summary Page**: Provides more granular allocations per product.
- Reports help visualize:
  - Direct allocations (e.g., Wealth charges CDPP $8M for account maintenance)
  - Corporate overhead allocations (no clear cost driver; bundled allocations pushed from corporate)

---

### 🔹 **Corporate Overhead Allocations**
- When costs can't be precisely attributed, they're bundled and pushed to LOBs.
- Shown under "Charges from Corporate" section in the report
- Key to understand when **direct allocations = 0** and corporate charges are applied instead

---

### 🔹 **Smart View Data Extraction**
- Uses **Smart View** to pull financials from a data environment (possibly Oracle/Hyperion).
- Extract includes:
  - ~5-6 columns of raw data
  - Monthly data
- Mapping files created to:
  - Identify **LOB**
  - Identify **Product**
  - Attribute **driver** and **processing log**

---

### 🔹 **Mapping Files & Keys**
- Mapping keys help:
  - Tie allocations to drivers (e.g., maintenance activities)
  - Roll up data to different levels (low-level → high-level views)
  - Identify owning and charging group
- Typical mappings:
  - `Processing Owning Log`
  - `Product Ownership`
  - `Driver (Driver5P for rollup)`
  - `LOB-Product Combination`

---

### 🔹 **Report Hierarchy Example**
- Example: CDPP product
  - Appears as one entity in the front-end report
  - In backend, has multiple LOB and product combinations for detailed tracking
- Data is summarized for reporting purposes, but full granularity exists in back-end mapping

---

### 🔹 **Data Flow Overview**
1. **Smart View Pull** → Extracted base data
2. **Mapping Applied** → Processing ownership, drivers, hierarchy
3. **Adjustments Made**:
   - **Manual Adjustments**
   - **Initiative-based Reallocations** (e.g., training programs, upskilling)
4. **Master Excel File** consolidates:
   - FY actuals
   - Forecasts (QF)
   - Initiatives
   - Manual adjustments
   - Baseline costs
5. **Final Output**: Shared reports, dashboards used by stakeholders

---

### 🔹 **Forecast Tabs & Adjustments**
- **Forecast Tab (HYP/SD Forecast)** contains:
  - High granularity data (e.g., salaries, benefits)
  - Manual adjustments made monthly
  - Initiative-based adjustments (future programs are excluded from current cost views)
- Examples: “Upskill Employee” costs are shifted from salary to initiative bucket

---

### 🔹 **Automation & Deliverables**
- Monthly report refreshes
- Changes happen by updating:
  - Workbook names
  - Driver columns
- Formula-driven master files reduce manual effort
- Goal: **Streamline reporting and automate mapping** for accuracy and repeatability

---

### 🔹 **Tools & Technical Stack**
- **Smart View** (pulls data)
- **Excel with Mapping Files** (transformations)
- **Oracle or Hyperion Planning (HYP)** (source system)
- **SQL knowledge is helpful** for advanced data manipulation

---

### 🔹 **Miscellaneous Notes**
- Reports often referred to as "Expense Packs"
- FY24 Actuals and FY25 Projections compared for YOY or MoM trends
- Final outputs shared with FP&A, finance ops, and leadership
- Reporting team tracks categories like salaries, rent, internal costs, and overhead

---

## 🔹 1. **Consolidated Metric Definitions Document**
- An Excel file has been created by the speaker to document:
  - **Data sources** – where the numbers come from (e.g., SmartView)
  - **Pulling methods** – how to extract data
  - **Formula logic** – definitions and meaning of metrics
  - Goal: Make understanding formulas, terminologies, and sources easier across stakeholders.

---

## 🔹 2. **NBS Report (Monthly Business Summary)**
- Shared with CFO of TD; includes:
  - **PNL Metrics** (Profit and Loss metrics)
  - **Ratios** for financial analysis
  - **Latest Month View** (e.g., March metrics shown in April)
  - Comparisons across:
    - Same month LY
    - Same quarter LY
    - YoY and QoQ metrics

---

## 🔹 3. **Key Revenue Components**
### 🟩 Net Interest Income (NII)
- Revenue generated from:
  - Loans (e.g., home equity, mortgages, consumer loans)
  - Credit cards (unsecured lending)
  - Bank deposit earnings (low/high interest savings)
  - Investments by the bank
- NII is broken down into source LOBs (Line of Business)
  - Residential Lending
  - Credit Card
  - Retail Deposit & Services

### 🟩 Fee-Based Income
- Revenue from services:
  - ATM charges
  - Account maintenance fees
  - Overdraft/penalties
  - Any non-interest earnings
- Together with NII, these form **Total Revenue**

---

## 🔹 4. **Deductions & Expense Metrics**
### 🟥 Provision for Credit Losses (PCL)
- Losses due to customer defaults (e.g., missed credit card payments)
- Treated as a bank expense

### 🟥 Operating Expenses (Opex)
- Salaries, rent, marketing, utilities, office supplies
- All costs to run banking operations

---

## 🔹 5. **Calculation Logic**
- **Net Income = Revenue - (PCL + Expenses)**
- Taxes are subtracted after net income to get final profit

---

## 🔹 6. **LOBS & Hierarchy**
- Think of LOBs as a **tree structure**:
  - Top: **Total Consumer & Commercial**
  - Consumer breaks into:
    - Residential Lending
    - Unsecured Lending (Credit Cards)
    - Retail Deposits
  - Each LOB has multiple **products**
- Some data may fall into “Others” bucket due to:
  - Incorrect segment tagging
  - Data integrity issues

---

## 🔹 7. **Key Financial Ratios & Metrics**
### 📊 ROE (Return on Equity)
- Formula: `Net Income / Allocated Capital`
- Tells how much income was generated from allocated investments
- Often annualized using:
  - Monthly NE and Capital values

### 📊 Net Interest Margin (NIM)
- Formula: `Net Interest Income / Average Balance`
- Shows earnings on deposit balances held by the bank

### 📊 Efficiency Ratio
- Formula: `Total Expenses / Total Revenue`
- Lower is better; ~50-60% is healthy for banks
- Shows how efficiently the bank is operating

### 📊 Operating Leverage
- Formula: `% Revenue Growth - % Expense Growth`
- Indicates the ability to grow revenue faster than expenses

---

## 🔹 8. **SmartView & Data Flow**
- Data is pulled from:
  - **SmartView** (likely Oracle/Hyperion-based)
  - PPM systems (Project Portfolio Management)
- Actuals are updated monthly
- Forecasts are updated quarterly by the bank
- The workbook contains:
  - 20–30 sheets (for NII, Fee, Expenses, etc.)
  - Centralized control tabs and dependency tracking
  - SmartView refresh pulls the latest data
- Working files not client-facing → used for calculation and internal review

---

## 🔹 9. **Rolling Forecasts (ROF)**
- Forecasting logic:
  - **Actuals till current month** (e.g., Feb)
  - **Forecast from next month onward** (e.g., Mar–Oct)
- Quarterly updates: Bank revises forecasts based on performance
- Actuals override forecast once available (e.g., Jan–Mar becomes actual in Q2)

---

## 🔹 10. **Expense Categories**
- Categories shown in reports include:
  - **Salaries**
  - **Occupancy** (rent, utilities)
  - **Marketing & Communication**
  - **Project/Initiative Costs**
- These are grouped and tracked via expense sheets

---

## 🔹 11. **Practical Tips & Usage**
- Final reports use **structured summaries**, while working files are extensive
- Formula references (e.g., for ROE, NIM) are maintained in an Excel tab for ease
- Speaker suggests reviewing sheets and not worrying about memorizing everything immediately
- Suggested approach: review and build understanding over time; deep dives scheduled for Tuesday sessions

---

Here are detailed and structured notes from **Session 3** of the MDS Knowledge Session. This session dives deeper into the **SmartView system architecture**, **data flow**, **rolling forecast logic**, **data cubes**, and **hierarchical navigation** in financial reporting. These notes build upon concepts discussed in earlier sessions.

---

## 🔹 1. **Session Overview**
- Primary focus: **Hands-on walkthrough** of the financial reporting structure via SmartView and SBase.
- Emphasis on:  
  - Working file walkthrough  
  - How SmartView connects to different cubes  
  - Difference between rolling forecasts and static forecasts  
  - Source of truth for top-of-house metrics

---

## 🔹 2. **SmartView Data Sources**
### ✅ **Key Cubes**
- **Product**: Holds most bank-level transactional data (e.g., revenue, expense at product level)
- **PQ (PU Cube)**: Aggregated operational and LOB (Line of Business) level data
- **Hyperion**: Main source for forecasts (Q1F, Q2F, etc.)

### ✅ **Why Multiple Cubes Exist**
- Banks have:
  - Multiple LOBs (consumer, commercial, wealth, sweep)
  - Data entry at different levels (e.g., consumer vs. consolidated)
- Forecast and actuals need different handling → split across cubes
- Cubes fetch from underlying systems (e.g., loans, deposits, third-party data)

---

## 🔹 3. **Forecast vs. Rolling Forecast**
### 🧮 **Forecast (QxF)**
- Generated **once per quarter** (e.g., Q2F at the end of April)
- Covers **Jan–Oct forecast values**
- Used for comparison and planning

### 🔄 **Rolling Forecast**
- **Actuals till current month** (e.g., March)
- **Forecast from next month onward** (e.g., April–October)
- Used in almost **all reports**; considered the primary planning structure
- Bank users compare rolling forecast with static QxF to evaluate forecasting accuracy

---

## 🔹 4. **Working with SmartView**
### 🧩 **Workflow Steps**
1. **Connect to SmartView panel**
2. Select **data source** (e.g., PQ or Product Cube)
3. Fill SmartView filters with:
   - Owning Org
   - Product
   - Account
   - Account Type (e.g., non-interest expense)
   - Month/FY
   - Version (actual, forecast)
4. **Refresh** → Populates data

### 🗂 **Equivalent to SQL Query**
- SmartView works like a structured SQL query:
  ```sql
  SELECT * 
  FROM Table 
  WHERE 
    owning_org = 'Consumer Excluding Wealth' AND 
    account = 'Total Expense' AND 
    month = 'November' AND 
    version = 'Actual'
  ```

---

## 🔹 5. **Hierarchical Navigation in SmartView**
- **"Zoom In"**: Drills down into deeper product hierarchies (e.g., unsecured lending → credit cards → individual card programs)
- **"Zoom Out"**: Moves up hierarchy (e.g., from card level to retail LOB)
- **Hierarchy Tree**:
  ```
  All LOBs
  ├── Consumer Excl. Wealth
  │   ├── Retail Deposit
  │   ├── Residential Lending
  │   └── Unsecured Lending (Credit Cards)
  └── Commercial
  ```

---

## 🔹 6. **Top-of-the-House (ToH) Numbers**
- Numbers representing **total for the bank** (e.g., total revenue, total expenses, etc.)
- Must match CFO's records exactly
- Retrieved from **Flash Reports**, not SmartView (due to ongoing discrepancies)
- Contacts: Heather, Michel (key stakeholders for ToH numbers)
- **Accuracy down to the million is critical** – senior leadership uses this for review

---

## 🔹 7. **Challenges and Adjustments**
### 🛠 **Manual Adjustments**
- Done for last-minute errors or reconciliation gaps
- May relate to:
  - Expense misclassifications
  - Wealth or Sweep numbers from alternate sources
  - Rounding differences across quarters

### ⚠ **Dual-Year Cubes**
- You’ll see both:
  - `2021` (locked version used for reporting at year-end)
  - `2022-2021` (adjustments made in 2022 for FY21)
- Helps preserve historical integrity while allowing corrections

---

## 🔹 8. **Productivity PL Report**
- Another source file used for:
  - Employee counts (FTEs)
  - Detailed breakdowns for Wealth & Sweep LOBs
- Shared by client (e.g., Matt Downing) for internal validation

---

## 🔹 9. **Key Concepts to Remember**
- **SBase = SmartView = Oracle Essbase backend**
- SmartView is Excel-based but connects to multi-dimensional OLAP cubes
- Always verify:
  - Cube used (PQ, Product, Hyperion)
  - Data version (actual, forecast, QxF)
  - Source of truth for sensitive numbers (e.g., ToH → Flash Report)
- **Monthly refreshes** are conducted in the first week of each month (e.g., April 7–9 for March data)

---

## 🔹 10. **Next Steps for You**
- Await SmartView + cube access
- Hands-on session promised (zooming, data pull, mapping)
- You may be able to **log in on their system** during breaks to practice

---

Let me know if you’d like:
- A glossary of cube terms (e.g., PQ, Hyperion, SBase)
- A flowchart of how data moves across systems and reports
- An annotated SmartView screenshot to walk through a pull

---

## 🔍 **MDS Knowledge Session Notes**

---

### **Session 1: Allocation Reporting & Expense Tracking**

#### 🔹 **Line of Business (LOB) and Allocation Types**
- Businesses incur costs and transfer those to other divisions (e.g., consumer and commercial).
- **Types of Allocations:**
  1. **Direct Allocations** – Attributed to specific products or services (e.g., 300M for account maintenance).
  2. **Corporate Overhead Allocations** – Bulk costs distributed without detailed methodology.

#### 🔹 **Reports and Views**
- **M3 Report**: Tracks allocations (actuals), shows split by LOB, products, and chargebacks.
- **SmartView**: Tool used to pull financial data, perform mapping, and link to Excel-based reporting.
- **DF Environment**: Book of record (DF = Data Foundation?).
- **Drilldowns**: Breakdown by consumer (residential lending, credit cards), commercial, etc.

#### 🔹 **Mapping & Keys**
- Mapping involves linking processing work, owning LOB, hierarchy, and product cross combinations.
- Multiple levels of granularity exist (e.g., product + owning LOB).
- Mapping maintained in separate Excel files using lookup logic.

---

### **Session 2: P&L Metrics & Efficiency Ratios**

#### 🔹 **Key Metrics in P&L Reporting**
- **NII (Net Interest Income)** = Interest earned from loans, deposits, credit cards.
- **Fee-Based Income** = Maintenance fees, ATM charges, etc.
- **PCL (Provision for Credit Losses)** = Credit card fraud/defaults.
- **OPEX (Operating Expense)** = Salaries, infrastructure, promotional costs.

#### 🔹 **Total Revenue & Net Income**
- **Total Revenue** = NII + Fee-Based
- **Net Income** = Revenue - (PCL + Expenses)
- **After-Tax Net Income** = Net Income - Taxes

#### 🔹 **Efficiency Ratios**
- **ROE** = Net Income / Allocated Capital (annualized)
- **Net Interest Margin (NIM)** = NII / Average Balance
- **Efficiency Ratio** = Total Expense / Total Revenue
- **Operating Leverage** = Revenue % growth - Expense % growth

#### 🔹 **Segment Views**
- Products categorized into:
  - Consumer: Credit Card, Residential Lending, Deposits
  - Commercial: Loans, Deposits
  - Others: Unidentified entries

---

### **Session 3: Forecasting, SmartView Cubes, and Rolling Forecasts**

#### 🔹 **Forecasting Logic**
- **Rolling Forecasts** = Actuals till current month + Forecasts for future months
- **Forecast Versions**:
  - Q1F = Jan-Oct
  - Q2F = Apr-Oct (received in May)
  - Q3F = Jul-Oct
  - Q4F = Oct Forecast Only
- **QNF vs Forecast**:
  - Forecast refers to static versions.
  - Rolling forecast is widely used in reports.

#### 🔹 **SmartView Cubes**
- **Product Cube** – Source for actuals
- **Hyperion Cube** – Source for forecasts
- **PQ Cube** – Intermediate structure with consolidated data

#### 🔹 **Top of the House Data**
- Comes from external reports (e.g., Flash, Productivity PL, not SmartView).
- Manual adjustments are made when SmartView/PQ data doesn’t match known top-line figures.
- Very senior stakeholders (e.g., SVP CFO) closely monitor this data.

#### 🔹 **Challenges**
- Frequent manual adjustments.
- Discrepancies between PQ and Flash reports.
- SmartView connection and refresh sensitivity (no Ctrl+Z after refresh).

---

### **Session 4: Deep Dive into Working Files & Product-Level Insights**

#### 🔹 **Working File Replication**
- Top of the house (ToH) numbers pulled from Flash reports.
- Wealth & Sweep from Product P&L reports.
- Custom sheets for each metric: NII, Fees, PCL, Volumes, Expenses.

#### 🔹 **SmartView Refresh Mechanics**
- Refreshing from SmartView pulls data using filters like:
  - Owning Org
  - Product
  - Account
  - Version
  - Account Type
- Drill-down: From LOB → Products → Sub-products → Final GL-level data.

#### 🔹 **Retail Deposits Breakdown**
- CDPP (Retail Deposit Products) includes sub-products:
  - Non-interest checking
  - Interest checking
  - MMA
  - CDs
  - Others
- Used to derive total consumer deposits.

#### 🔹 **Parameterization & Templates**
- Input Parameter Sheet: Drives all reporting workbooks.
- Changing one parameter (e.g., forecast version, period) updates all linked sheets.
- Controlled refresh using macro scripts.

#### 🔹 **Reporting Metrics & Views**
- Consumer segments: CDPP, Residential Lending, CCU, Wealth, TDAF.
- Total Expense = Opex + Allocations
- Allocations come from indirect contributors (e.g., tech, transformation teams).

---

Here are the structured notes for **MDS Knowledge Session 4**:

---

### 🔍 **Session Focus:**
- Understanding how financial metrics are pulled and structured in Excel using SmartView (Essbase).
- Breaking down and calculating components for metrics like **NII**, **Total Expenses**, and **Consumer Deposits** using product-level cubes.
- Explaining **data sources**, **forecasting logic**, and the **input parameter linkage** in financial models.

---

### 📊 **Data Flow and SmartView Integration:**

- **Top of the House (TOH) Numbers**:
  - **Loans, Deposits, and NII** for TOH are not fetched from SmartView/PA due to discrepancies.
  - They come from:
    - **Flash Report** – maintained by Heather or Michel (TOH loans/deposits/NII).
    - **Product PL Report** – for Wealth & Sweep metrics (Matt maintains it).

- **Working File Structure**:
  - Mirrors the MDS final output file.
  - Contains linked sheets for each metric (NII, Opex, CDPP, etc.).
  - Sheet links often break if renamed; macros are being built to address this.

---

### 🧩 **Key Concepts Explained:**

- **SmartView & Essbase**:
  - Connected via “SIS Cluster” > select appropriate cube (e.g., PQ, Product).
  - Cubes like `PQ 2023`, `Product`, and `Hyperion` contain Actuals and Forecast data.
  - Always clone a working sheet before refreshing (no Ctrl+Z post-refresh).

- **Zoom-In/Drill-Down Functionality**:
  - Can zoom into **Org Unit > Product > Account > Processing Level**.
  - Example: NII from `Consumer Excl. Wealth` > Zoom into Product hierarchy → Residential Lending → Credit Cards.

- **Identifying Unmapped Values**:
  - “Non-product related” or “Unidentified” incomes/expenses are grouped and tracked.
  - You can ask Mike (team POC) or search NorthStone team’s documentation to resolve such values.

---

### 📈 **CDBP & Consumer Metrics**:

- **CDBP Composition**:
  - Formed using **Retail Deposit Product**, **Private Banking Product**, **Retail Banking Services Product**.
  - Contains sub-products: Non-Interest Checking, Interest Checking, MMAs, CDs, etc.

- **NII Decomposition**:
  - For Consumer: Includes Residential Lending, Credit Cards, Auto Loans (TDF), and Consumer Excl. Wealth.
  - Derived using combinations from SmartView selections based on Org Unit, Product, and Account.

---

### 💸 **Expense Calculations**:

- **Opex vs. Total Expense**:
  - **Opex** = Operational cost (branches, checks, ATMs).
  - **Total Expense** = Opex + Allocation (indirect costs for shared services).
  - Allocation examples: Essex analytics teams working across multiple orgs.

- **Opex Source**:
  - Derived from **Deposit Products** only.
  - Line references from “Admin Sheet” used to identify which rows contribute to Opex vs. Total Expense.

---

### 🔄 **Forecasting & Automation**:

- **Input Parameter Sheet**:
  - Controls which month/quarter to refresh.
  - Changing values (e.g., from Feb to Mar) will automatically update all linked metric sheets via formulas/macros.

- **Forecast Type Handling**:
  - Actuals till current month, Forecasts for rest.
  - Refresh logic takes into account if data is from Q1F, Q2F, etc.

---

### 🛠️ **Best Practices & Warnings**:

- Never refresh SmartView on a working sheet—clone it instead.
- Use “Suppress Missing Data” in SmartView to clean up empty product rows.
- Be mindful of alias changes; always set member display to **Default**.

---

### ✅ **Action Items / Reminders**:

- Explore zoom-in logic in SmartView for Org/Prod/Account.
- Understand how CDBP products are linked to different metrics.
- Familiarize yourself with Admin Sheets for identifying Opex lines.
- Ask for the latest **Input Parameter macro file** in the next session.
- Prepare questions for Session 5.

---
