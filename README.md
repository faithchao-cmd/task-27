# Executive Sales Dashboard (Power BI)

A one-page executive KPI dashboard with dynamic filters, built from a US sales dataset (3,000 order lines, Jan 2023 – Dec 2024).



## Business questions
- How are sales, profit and margin trending, and are we growing year over year?
- Which categories, regions and products drive results?
- Where are we losing money?

## Key findings
- Sales **$3.14M**, profit **$540.9K**, margin **17.2%**, **2,998** orders, AOV **$1,048**.
- 2024 was weaker than 2023: sales **-4.8%**, profit **-6.2%**.
- **Discounting is the main margin problem:** 0% discount = 25.7% margin; 30% discount = -6.9% margin, with 68% of those lines losing money.
- **Concentration risk:** one product (Multifunction Copier) is ~40% of revenue.
- Margins are even across categories (16.8-17.5%); South is best at 19.2%.

## KPIs (6)
| KPI | Definition |
|---|---|
| Total Sales | Sum of Sales |
| Total Profit | Sum of Profit |
| Profit Margin % | Profit / Sales |
| Orders | Distinct Order ID + Customer ID |
| Avg Order Value | Sales / Orders |
| Sales YoY % | (Sales 2024 - Sales 2023) / Sales 2023 |

> Note: Order ID alone repeats across customers and regions (about 4 lines each), so an order is defined as Order ID + Customer ID. This matches the AOV of ~$1,048 in the source workbook's KPI Summary.


## How to build it in Power BI
1. **Get data:** load `Sales_Data.xlsx`, sheet *Sales Data* (or the clean CSV). In Power Query set `Order Date` and `Ship Date` to *Date* (US locale), then Close & Apply.
2. **Date table:** create it with the DAX in `DAX_Measures.txt`, mark it as the date table, sort `Year-Month` by `Year-Month Sort`.
3. **Relationship:** `Date[Date]` (1) to `Sales Data[Order Date]` (*), single direction.
4. **Measures:** paste from `DAX_Measures.txt`. Format Profit Margin % and YoY as percentages.
5. **Visuals:**
   - 6 KPI cards (Sales, Profit, Margin %, Orders, AOV, Sales YoY %)
   - Line and clustered column: X = `Date[Year-Month]`, columns = Total Profit, line = Total Sales
   - Clustered bar: Category by Profit Margin %
   - Clustered bar: Region by Total Sales
   - Clustered bar: Sub-Category by Total Profit
   - Column chart: Discount by Profit Margin %
6. **Slicers:** Year, Region, Segment, Category. Check *Edit interactions* so each slicer filters every visual.
7. **Polish:** white or light-grey background, navy accent, red only for negatives, remove gridlines, align and distribute visuals, takeaway titles.

## Design principles
Limit KPIs, one message per visual, consistent colours and formats, summary then trend then breakdown, detail on drill-through pages.

## Tools
Power BI Desktop, DAX, Power Query. Excel for source data.
