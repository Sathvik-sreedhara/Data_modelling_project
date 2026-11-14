# Enterprise Data Modeling in Power BI (Star Schema and RLS)

A Power BI project that turns a **23-table dataset with many-to-many relationships** into a clean **star schema** (6 dimension tables, 6 fact tables), validates the numbers against control totals, and secures the report with **region-based row-level security (RLS)**.

<!-- Add a screenshot of the model view at images/data_model.png, then uncomment the next line -->
<!-- ![Star schema model view](images/data_model.png) -->

<!-- Dataset source: add the dataset name and link here (for example, "Source: <name>, <link>") -->

## Problem

The source data came as 23 related tables connected through many-to-many relationships. Reporting directly on that structure is risky:

- Many-to-many relationships make filters behave unpredictably.
- Duplicate or test records inflate totals.
- A join through duplicate product records can **multiply fact rows (fan-out)**, which overstates revenue.

The goal was a model where every measure gives one consistent, verifiable answer.

## Approach

### 1. Dimensional modeling
Restructured the 23 tables into a star schema with **6 dimension tables and 6 fact tables**, replacing many-to-many relationships with one-to-many relationships from dimensions to facts.

### 2. Data preparation (Power Query / M)
- Merges, splits, unpivots, and list expansion to reshape source tables
- Removed test records, duplicates, and unused fields

### 3. Validation
- Compared **control totals** between the source data and the model
- Traced a **revenue fan-out** to duplicate product records: the duplicates caused matching fact rows to be counted more than once, inflating revenue. Cleaning the duplicates and re-checking control totals confirmed the model reported the correct figures

### 4. DAX measures
| Measure | Purpose |
|---|---|
| Sales | Total sales value |
| Distinct Orders | Number of unique orders |
| Active Customers | Customers with activity in the selected context |
| Order-to-Payment Days | Days between order and payment |

### 5. Row-level security
Implemented **region-based RLS** using `USERPRINCIPALNAME()`, so each signed-in user only sees data for their region.

To test: in Power BI Desktop, go to **Modeling > View as**, select the role, and check that visuals filter to that region.

## Repository Contents

| File | Description |
|---|---|
| `portfolio_data_model.pbix` | Power BI model, Power Query steps, DAX measures, and RLS roles |
| `LICENSE` | MIT |

## How to Open

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
2. Open `portfolio_data_model.pbix`.
3. Use **Model view** to see the star schema, **Transform data** to see the Power Query steps, and **Modeling > View as** to test RLS.

## Skills Demonstrated

Dimensional modeling (star schema) · Power Query (M) · DAX · Data validation with control totals · Row-level security · Debugging fan-out in a data model

## Author

**Sathvik Sreedhara** · [LinkedIn](https://www.linkedin.com/in/sathvik-sreedhara-0a37272b6) · [GitHub](https://github.com/Sathvik-sreedhara)
