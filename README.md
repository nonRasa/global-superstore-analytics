# Global Superstore Analytics

An end-to-end analytics project built around the Global Superstore dataset. The project combines data warehousing, statistical analysis, machine learning, and an executive Power BI dashboard to produce practical business insights.

## Project Objectives

The project has four primary deliverables:

1. Load the source data into MySQL and build a star-schema warehouse in Power BI.
2. Test whether discounted items have a statistically significant difference in sales quantity.
3. Train generalizable machine-learning models to predict `Profit` and `Ship Mode`.
4. Build a management dashboard that answers the required business questions and provides actionable recommendations.

> Data cleaning, preparation, and the construction of Fact and Dimension tables must be performed in Power BI and Power Query. Python is reserved for the statistics and machine-learning phases.

## Data Source


The archive contains `Superstore.sql`, which creates the following MySQL source tables:

| Source table | Grain | Primary key |
|---|---|---|
| `product` | One row per product | `Product ID` |
| `customer` | One row per customer | `Customer ID` |
| `order` | One row per order | `Order ID` |
| `order_detail` | One product line per order | `Row ID` |
| `returned` | One row per returned order | `Order ID` |
| `shipping` | One row per shipment | `Shipping ID` |

Before running the SQL file, create a dedicated MySQL database and add the following statement to the beginning of your local copy:

```sql
USE YOUR_DB_NAME;
```

The SQL file contains `DROP TABLE IF EXISTS` statements. Run it only against the dedicated project database. Raw data files are intentionally excluded from Git.

## Proposed Data Warehouse

The central table is `FactSales`, with one row per product line in an order. The proposed dimensions are:

- `DimProduct`
- `DimCustomer`
- `DimDate`
- `DimGeography`
- `DimShipMode`
- `DimMarket`
- `DimOrderPriority`

The fact table contains the business measures `Sales`, `Quantity`, `Discount`, `Profit`, and `ShippingCost`, along with calculated fields such as `ShippingDays` and `IsReturned`.

All relationships should be one-to-many from dimensions to the fact table with single-direction filtering. The detailed design is available in [`database/design/star-schema.md`](database/design/star-schema.md).

## Statistical Analysis

The discount analysis divides sales lines into two groups:

- Discounted items: `Discount > 0`
- Non-discounted items: `Discount = 0`

The analysis should include distribution checks, descriptive statistics, a suitable hypothesis test, confidence intervals, effect size, assumptions, and a business interpretation of the result.

## Machine Learning

### Profit Regression

Train and compare regression models that predict `Profit`. The workflow should include a baseline, leakage-safe preprocessing, feature selection, cross-validation, holdout evaluation, overfitting checks, and interpretable error analysis.

### Ship Mode Classification

Train a multiclass model that predicts `Ship Mode` at the order level. Features that are generated after the shipping decision must be excluded to prevent target leakage. Report class balance, a confusion matrix, per-class metrics, macro-averaged metrics, and test-set performance.

## Dashboard Requirements

The Power BI report should include the statistical and machine-learning results and answer the following management questions:

- What is the size of each market based on total and average sales?
- Which markets are the strongest investment candidates?
- What is the relationship between order value and shipping cost?
- What is the average delivery time by ship mode, country, and region?
- Which day of the week generates the highest sales?
- Which categories, subcategories, and products generate the highest profit?
- How does each product's profit differ from the overall average, and which regions benefit most?
- What additional actions could increase sales or improve profitability?

Recommended additional analyses include return-rate profitability and customer segmentation using RFM.

## Repository Structure

```text
.
├── .github/                 # Issue and pull-request templates
├── data/
│   ├── raw/                 # Local source files; ignored by Git
│   └── processed/           # Generated analysis data; ignored by Git
├── database/
│   └── design/              # Warehouse and star-schema design
├── docs/                    # Project plan and decisions
├── models/                  # Trained model artifacts; ignored by Git
├── notebooks/               # Statistics and machine-learning notebooks
├── powerbi/
│   ├── dax/                 # Exported DAX measures
│   └── power-query/         # Exported Power Query M scripts
├── reports/
│   ├── figures/             # Generated charts; ignored by Git
│   └── outputs/             # Metrics and predictions; ignored by Git
└── src/superstore/          # Reusable Python modules
```

## Recommended Workflow

Use `main` as the stable branch and create one branch per task, for example:

- `feature/powerbi-star-schema`
- `feature/statistics-discount`
- `feature/ml-profit-regression`
- `feature/ml-shipmode-classification`
- `feature/dashboard`

Open a pull request for each completed task and request review from at least one teammate. Because Power BI files are binary, coordinate ownership of the `.pbix` file and avoid editing it concurrently.

## Project Status

- [x] Source schema reviewed
- [x] Initial repository structure created
- [ ] Power BI data-quality workflow completed
- [ ] Star schema implemented and validated
- [ ] Statistical analysis completed
- [ ] Profit regression model completed
- [ ] Ship Mode classification model completed
- [ ] Dashboard and final presentation completed
