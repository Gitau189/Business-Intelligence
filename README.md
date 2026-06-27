# DSA 3050A – Business Intelligence & Visualization
## Mid-Semester Practical Examination Dashboard

### Student Information
- **Student Name:** Collins Gitau Waiya
- **Course Code:** DSA 3050A
- **Assignment:** Mid-Semester Practical Examination
- **Submission Date:** June 27, 2026

---

### 1. Dataset Specifications & Integrity Verification
- **Dataset Name:** Global Superstore Enterprise Data
- **Source URL:** Public Domain Data Repository (Legitimate Public Business Dataset)
- **Scale:** 51,290 Records | 24 Baseline Structural Columns
- **Academic Honesty Affirmation:** This dataset consists of real-world historic multinational retail transactional data. No synthetic, AI-generated, or artificially inflated records have been utilized.

---

### 2. Core Business Problem Under Analysis
The executive leadership team requires a comprehensive diagnostic business intelligence solution to analyze global supply chain efficiency, product vertical margins, and geographic sales distributions. 

The primary business objective is to identify:
- Operational distribution bottlenecks and margin leakages across regional corridors.
- High-frequency product return anomalies causing bottom-line compression.
- The logistical impact of shipping modes and delivery timeframes on net profitability.

---

### 3. Comprehensive Power Query Data Transformation Log

A rigorous data preparation lifecycle was executed within the Power Query Editor to transition the raw tables into an analytical schema. The specific **Applied Steps** completed include:

#### A. Basic Data Cleaning & Schema Standardization
- **Column Schema Alignment:** Renamed cryptic database markers to intuitive descriptive titles (e.g., standardized `Postal Code` handling). Removed administrative database fields such as `Row ID` to reduce data model weight.
- **Type Casting:** Enforced explicit static typing across all variables. Transformed monetary metrics (`Sales`, `Profit`, `Shipping Cost`) into **Fixed Decimal Numbers**, quantity indices into **Whole Numbers**, and transactional timestamps into strict **Date** types.
- **Data Integrity Enforcement:** Ran global deduplication logic across all primary transaction composites to eliminate duplicate records. Executed structural row-purging to drop empty records and blank data lines.
- **Text Normalization:** Applied institutional text sanitation by running `Trim` and `Clean` operations across all string dimensions (`Customer Name`, `Segment`, `Category`, `Sub-Category`) to eliminate trailing white spaces or unprintable non-unicode data formatting anomalies.
- **Inconsistency Mitigation:** Identified null international values within the `Postal Code` field for regions outside the United States and replaced them with a uniform string placeholder (`00000`) to preserve operational integrity without discarding critical rows.

#### B. Intermediate & Advanced Structural Engineering
- **Column Splitting:** Isolated the country and structural regional prefixes out of the composite `Order ID` attribute using custom text delimiter splitting rules.
- **Field Merging:** Combined the `Category` and `Sub-Category` text fields into a unified attribute named `Product_Class` to serve as a high-density matrix grouping element.
- **Calculated Custom Attributes:** Formulated a custom transactional metric tracking fulfillment velocity:
  `Delivery_Days = [Ship Date] - [Order Date]` (Casted to Whole Number).
- **Conditional Logic Segmentation:** Structured a multi-tier logic rule to flag organizational performance states inside a new column named `Profitability_Status`:
  - *If `Profit` > 0 $\rightarrow$ "Profitable"*
  - *If `Profit` < 0 $\rightarrow$ "Loss-Making"*
  - *Else $\rightarrow$ "Break-Even"*
- **Temporal Dimension Decomposition:** Extracted critical date parts from `Order Date` into explicit separate attributes: `Order_Year`, `Order_Month`, `Order_Quarter`, and `Order_Day`.
- **Relational Query Merges:** Executed a **Left Outer Join** combining the main `Orders` table with the `Returns` table using `Order ID` as the relational key, expanding the table to capture the `Returned` status vector globally.
- **Summarized Query & Group By Aggregations:** Developed a separate high-level view named `Category_Performance_Summary` using the **Reference Query** method. Applied advanced `Group By` clauses to aggregate `Total_Sales` (Sum) and `Total_Profit` (Sum) categorized by core commercial product verticals.

---

### 4. Interactive Dashboard Architecture
The front-end user interface is built using a professional high-contrast layout featuring an executive dark slate canvas background (`#202529`) overlaid with elevated white chart cards with `8px` rounded corners and drop-shadow styling to ensure rapid readability.

#### Implemented Visualization Matrix:
1. **Summary Banner Cards:** Three interactive KPI cards displaying aggregated `Total Sales`, `Total Profit`, and `Total Quantity Ordered`.
2. **Product Performance Analysis:** Horizontal **Clustered Bar Chart** detailing total sales distribution across individual `Sub-Categories`.
3. **Strategic Margin Analysis:** Vertical **Stacked Column Chart** breaking down profit composition by `Segment` paired with a categorical color legend.
4. **Fulfillment Volatility Overview:** Multi-tier relational **Matrix Visual** mapping macro `Regions` across rows and product `Categories` across columns to track profit densities.
5. **Geospatial Intelligence Map:** Bubble-size scaled **Geographic Map Visual** plotting sales distribution metrics directly across regional coordinates.
6. **Longitudinal Trend Vector:** Interactivity-enabled **Line Chart** displaying corporate sales performance plotted over time hierarchies.
7. **Volume Composition Proportion:** Executive **Donut Chart** evaluating macro revenue contributions split by product `Category`.
8. **Granular Ledger Lookups:** Low-level descriptive **Table Visual** hosting row-level detail verification options (`Order ID`, `Customer Name`, `Product Name`, `Sales`).

#### Interactivity Mechanisms Enforced:
- **Hierarchical Drill-Downs:** Activated structural multi-level date path exploration (`Year` $\rightarrow$ `Quarter` $\rightarrow$ `Month`) natively on the primary line chart trend vector.
- **Cross-Filtering Matrix:** Synchronized all charts to dynamically isolate visual slices instantly upon selecting specific segments across the donut or bar layouts.
- **Analytical Controls:** Provisioned three modular slicer dropdown bars covering `Year`, `Region`, and `Market` to afford immediate localized inspection capabilities.
