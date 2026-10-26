# E-Commerce Customers & Sales Analysis

An end-to-end data analysis project on a year of e-commerce orders (January to December 2023). I started with four messy raw tables, cleaned them with Python (pandas), combined everything into one analysis-ready table, and built a dashboard in Power BI to look at sales, returns, regions, products and payment methods.

![Dashboard](images/dashboard.png)

---

## The questions I wanted to answer

- How much did the business actually earn after returns?
- Which product categories and products drive most of the revenue?
- Which regions sell the most?
- How do sales and returns change month to month?
- How much money is lost to returns, and which categories are responsible?
- Do customers prefer one payment method over another?

---

## Headline numbers

| Metric | Value |
|---|---|
| Gross Sales | 89.71M |
| Return Value | 6.48M |
| **Net Sales** | **83.23M** |
| Total Orders | 4,500 |
| Return Rate | ~7% |

---

## What the dashboard shows

**Sales**
- **Furniture is the business.** It brings in roughly 63M of the 83M net sales, far ahead of Electronics, Clothing, Grocery and Stationery.
- At product level, Bookshelf and Sofa Set lead at around 12M each, followed by Office Chair and Dining Table. The top of the list is almost entirely furniture.
- **South** is the strongest region (about 27M), then West, North and East. A chunk of sales has no region recorded, which shows up as a separate "(Blank)" bar.
- Monthly net sales stay between about 5.6M and 8.7M. **April peaked** at 8.7M and **February was the weakest** month at 5.6M.

**Returns**
- Furniture also accounts for most of the returned value (close to 5M), which makes sense since it carries the highest prices.
- Monthly return value is fairly steady at about 0.5M to 0.6M, with a dip in March (0.35M).

**Payments**
- Orders are spread almost evenly across Cash on Delivery, Credit Card, UPI, Net Banking and Debit Card (roughly 18 to 19% each). About 18% of orders have no payment mode recorded, shown as "Unknown".

---

## How I built it

### 1. Cleaning the raw data (Python / pandas)

The raw files had the kind of problems you see in real data. Here is what I found and fixed:

| Table | Raw rows | Clean rows | Issues handled |
|---|---|---|---|
| customers | 1,225 | 1,200 | 25 duplicate customers, mixed date formats, inconsistent city casing (`KOCHI`, `Kochi`), missing phone / email / city |
| orders | 4,515 | 4,500 | 15 duplicate orders, mixed date formats (`31-03-2023`, `29/10/2023`), missing payment mode and ratings |
| order_items | 11,350 | 11,350 | Negative quantities marked as returns, so I added a `transaction_type` column (Sale / Return/Refund) |
| products | 40 | 40 | Category casing fixed (`electronics` to `Electronics`) |

Other cleaning steps:
- Standardised payment modes. `COD` and `Cash on Delivery`, `upi` and `UPI`, `NetBanking` and `Net Banking`, and `credit card` and `Credit Card` were all the same thing written differently.
- Converted all dates to a single `YYYY-MM-DD` format.
- Filled missing values with `Unknown` instead of dropping rows, so no sales were lost.

### 2. Building the data model

I joined the cleaned tables into one fact table, `fact_sales_dashboard.csv` (11,350 rows, one per order line), and created a date table, `dim_date.csv`, for time analysis.

Calculated columns in the fact table:

- `gross_sales`: value of sold items
- `return_value`: value of returned items
- `net_sales`: gross sales minus returns
- `sale_qty` / `return_qty`: units sold and returned

### 3. Dashboard (Power BI)

Built KPI cards, line charts for monthly trends, bar charts for category, product and region, a donut chart for payment mode, and a dark theme with green accents so the numbers stand out.

---

## Repository structure

```
ecommerce-sales-analysis/
├── data/
│   ├── raw/        # original files as received (customers, orders, order_items, products)
│   ├── clean/      # cleaned versions of the four tables
│   └── model/      # fact_sales_dashboard.csv and dim_date.csv used in Power BI
├── images/
│   └── dashboard.png
└── README.md
```

---

## How to explore it yourself

1. Clone the repo
   ```bash
   git clone https://github.com/<your-username>/<your-repo-name>.git
   cd <your-repo-name>
   ```
2. In Power BI Desktop, load `data/model/fact_sales_dashboard.csv` and `data/model/dim_date.csv`, then connect them on the date column.

---

## Tools used

- **Python** (pandas, numpy) for cleaning and transformation
- **Power BI** for the data model, DAX measures and dashboard
- **CSV** files for storage

---

## What I'd do next

- Look at customer-level behaviour: repeat buyers, lifetime value and which cities buy the most
- Dig into why furniture returns are so high (price, product, or region)
- Fix the missing region and payment data at the source so fewer rows end up as "Unknown"
- Add customer ratings to the dashboard

---

## About me

Built by **<Your Name>** as part of my data analyst portfolio.

- LinkedIn: <your-linkedin-link>
- Email: <your-email>

Feedback and suggestions are always welcome.
