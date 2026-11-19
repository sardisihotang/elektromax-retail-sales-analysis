# ElektroMax — Retail Sales & Customer Analytics Dashboard

> Portfolio project for learning data preparation, data modeling, KPI analysis, and interactive reporting with Microsoft Power BI.

## Project overview
This project explores a retail-electronics dataset for a fictional business named **ElektroMax**. The report is organized into three pages: Executive Overview, Product & Store, and Customer Analysis.

The workbook supplied for this project contains **7 tables** and covers **1 January 2023–31 December 2025**. The fact table contains **56,748 rows before duplicate-key handling**. The analysis baseline documented here removes duplicate primary keys from the fact table and normalizes transaction-status labels.

> **Learning disclosure:** This project was developed as a learning exercise using a YouTube tutorial as a learning reference. The tutorial/channel reference should be credited below. The project should not be presented as fully independent work if substantial steps followed the tutorial.

## Business questions
- How does net sales performance change over time?
- Which product subcategories contribute the most to net sales?
- How does sales contribution differ by store/region?
- Which customer segments contribute most to net sales?
- How are transactions distributed by payment method, promotion, and transaction status?

## Dataset
The supplied Excel workbook contains these sheets:
- `FACT_PENJUALAN`
- `DIM_PRODUK`
- `DIM_WAKTU`
- `DIM_PELANGGAN`
- `DIM_TOKO`
- `DIM_KARYAWAN`
- `DIM_PROMOSI`

**Dataset source:** [Add the original public dataset URL and its license/usage terms here.]

**Privacy:** Do not publish the original customer table. It contains direct identifiers such as customer names, email addresses, and phone numbers. Only publish a properly anonymized/aggregated dataset if redistribution is permitted by the source license.

## Tools
- Microsoft Excel — workbook inspection
- Power Query — data cleaning and transformation
- Power BI Desktop — data model, DAX measures, report pages, and visualization

## Data preparation
The supplied workbook was inspected for data types, missing values, duplicate primary keys, and inconsistent category labels.

Key observations:
- `FACT_PENJUALAN` has 56,748 rows and 20 repeated `penjualan_id` values.
- `DIM_PRODUK` has one repeated `produk_id`.
- Missing values occur in selected fields; they should be handled according to business meaning rather than deleting every row containing any blank.
- Transaction status variants `selesai`, `SELESAI`, `Done`, `Sukses`, and `Complete` are mapped to `Selesai`. Return-related variants should be mapped consistently to `Retur` if that mapping is used in the report.
- Customer direct identifiers must be removed or masked before any public sharing.

See [`documentation/data_cleaning.md`](documentation/data_cleaning.md) and [`documentation/data_dictionary.md`](documentation/data_dictionary.md).

## Data model
The workbook is structured as a fact table (`FACT_PENJUALAN`) with dimension tables for product, date, customer, store, employee, and promotion. See [`documentation/data_model.png`](documentation/data_model.png).

The diagram documents the intended key relationships based on matching ID columns. Confirm relationship cardinality and filter direction in the actual PBIX model before publishing.

## Dashboard pages
1. **Executive Overview** — headline KPIs and sales trend.
2. **Product & Store** — product subcategory, store, region, and margin comparisons.
3. **Customer Analysis** — customer segment, age group, gender, promotion, and payment-method views.

Screenshots should be placed in `screenshots/`:
- `executive_overview.png`
- `product_store.png`
- `customer_analysis.png`

## Initial findings from the supplied workbook
The following baseline is calculated from the workbook after keeping the first row for each `penjualan_id`, normalizing status labels, and including only normalized `Selesai` transactions. It is a **three-year dataset baseline**, not necessarily the same as a dashboard view filtered to 2024.

- Completed transactions: **48,182**.
- Net sales (`total_neto`): **Rp247,09 miliar**.
- Gross profit (`gross_profit`): **Rp76,31 miliar**.
- Gross profit margin, calculated as gross profit divided by net sales: **30.9%**.
- Highest net-sales subcategory: **Televisi** (Rp62,92 miliar).
- Next highest subcategory: **AC** (Rp60,28 miliar).
- Highest-contributing customer segment label: **Regular** (Rp124,32 miliar). Segment labels with different capitalization (e.g. `Regular` and `REGULAR`) must be standardized before treating them as one segment.

These are descriptive findings, not causal conclusions. Recalculate the figures after finalizing all cleaning rules and matching the exact report filters.

## Recommendations to investigate
- Review inventory and merchandising for the highest-contributing subcategories.
- Standardize customer segment labels before comparing segment performance.
- Evaluate promotion effectiveness using a clearly defined comparison group and net-sales/profit measures.
- Compare stores using consistent date, status, and net-sales filters.

## Limitations
- The workbook's public source URL and license have not been provided in this repository draft.
- The data contains missing values and inconsistent labels; decisions need to be documented and validated.
- Some customer records contain placeholder values such as `—`; these should not be interpreted as real demographic information.
- Dashboard values may differ from the three-year baseline if the report is filtered to a particular year or uses different status/KPI definitions.
- No causal impact of promotions or customer characteristics is established by this descriptive analysis.

## Learning reference
- YouTube channel: [Add channel name]
- Tutorial video: [Add video title and URL]

## How to explore
1. Open the published interactive Power BI report: [Add public dashboard URL].
2. Review the screenshots in `screenshots/`.
3. Open the PBIX file if it is included and you have Power BI Desktop installed.

## Author
**Sardianto Sihotang**  
[GitHub profile URL] · [LinkedIn profile URL]
