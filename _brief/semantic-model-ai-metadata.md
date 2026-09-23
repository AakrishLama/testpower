# Semantic Model AI Metadata

This companion guide records natural-language synonyms and routing guidance for the `scratch_from_warehouse` semantic model. Standard table, column, and measure descriptions are stored in the semantic model metadata. Synonyms and Prep data for AI recommendations are documented here because the current local authoring route does not expose a dedicated synonym property.

## Model vocabulary

| Preferred term | Meaning |
|---|---|
| Order | A distinct value of `fact_sales[OrderNumber]`; use `[Total Orders]`. |
| Order line | A row in `fact_sales` representing product detail within an order. |
| Quantity, units, ordered units, sales volume | `fact_sales[OrderQuantity]`; use `[Total Order Quantity]`. |
| Line-item activity | The model logic represented by `[Total Line Items]`; do not assume it is equivalent to a distinct row count without confirming the source definition. |
| Active customers | Customers with sales rows in the current filter context; use `[Active Customers]`. |
| Order date | The primary active date role through `fact_sales[OrderDateKey]`. |
| Stock date | The alternate inactive date role through `fact_sales[StockDateKey]`; use `[Stock Date Order Quantity]` when explicitly requested. |
| Product | A catalog item identified by `dim_product[ProductName]` or `dim_product[ProductSKU]`. |
| Category | `dim_product[CategoryName]`. |
| Subcategory | `dim_product[SubcategoryName]`. |
| Territory, geography, location | Attributes in `dim_territory`, especially Region, Country, and Continent. |

## Table synonyms

```yaml
tables:
  fact_sales:
    - sales
    - sales transactions
    - order lines
    - sales fact
    - transaction fact
  dim_customer:
    - customers
    - customer
    - customer profiles
    - customer dimension
  dim_product:
    - products
    - product
    - product catalog
    - merchandise
    - product dimension
  dim_date:
    - dates
    - calendar
    - date dimension
    - calendar table
  dim_territory:
    - territories
    - sales territories
    - geography
    - geography dimension
    - locations
```

## Measure synonyms

```yaml
measures:
  Total Orders:
    - order count
    - number of orders
    - sales orders
    - distinct orders
  Total Order Quantity:
    - units sold
    - quantity sold
    - ordered units
    - units ordered
    - sales volume
  Total Line Items:
    - line items
    - order line activity
    - line-item total
  Active Customers:
    - customers with orders
    - ordering customers
    - customer reach
    - distinct customers
  Last Order Date:
    - latest order date
    - most recent order
    - last sale date
  Total Order Quantity Previous Year:
    - prior-year quantity
    - previous-year units
    - last-year ordered units
    - prior-year sales volume
  Order Quantity YoY %:
    - year-over-year quantity growth
    - year-over-year units change
    - YoY quantity
    - annual quantity growth
  Stock Date Order Quantity:
    - quantity by stock date
    - stock-date units
    - units using stock date
    - stock timing quantity
```

## Column synonyms

```yaml
columns:
  fact_sales:
    OrderNumber:
      - order number
      - sales order
      - order ID
    OrderQuantity:
      - quantity
      - units
      - units sold
      - ordered quantity
    OrderLineItem:
      - line item
      - order line number
      - line sequence
    OrderDateKey:
      - order date
      - date ordered
      - purchase date
    StockDateKey:
      - stock date
      - inventory date
      - stock timing date
  dim_customer:
    FullName:
      - customer name
      - full customer name
      - buyer name
    BirthDate:
      - date of birth
      - birthday
    AnnualIncome:
      - income
      - yearly income
      - annual earnings
    TotalChildren:
      - number of children
      - children
    HomeOwner:
      - homeowner
      - home ownership
  dim_product:
    ProductSKU:
      - SKU
      - stock keeping unit
      - product code
    ProductName:
      - product
      - item
      - product label
    ModelName:
      - model
      - product model
      - model family
    ProductColor:
      - color
      - product colour
    ProductSize:
      - size
    ProductStyle:
      - style
    ProductCost:
      - cost
      - product cost
    ProductPrice:
      - price
      - product price
    CategoryName:
      - category
      - product category
    SubcategoryName:
      - subcategory
      - product subcategory
  dim_date:
    Year:
      - calendar year
      - year
    Month:
      - calendar month
      - month number
    Day:
      - day of month
      - calendar day
  dim_territory:
    Region:
      - sales region
      - territory region
    Country:
      - sales country
      - market country
    Continent:
      - geographic continent
      - sales continent
```

## AI routing guidance

Recommended instructions for Fabric Prep data for AI:

1. Use `fact_sales[OrderDateKey]` and `dim_date` as the default time context for order and quantity analysis.
2. Use `[Total Orders]` for order-count questions, not a raw row count.
3. Use `[Total Order Quantity]` for quantity, units, or sales-volume questions.
4. Treat orders, order lines, and quantity as different concepts.
5. Use `[Stock Date Order Quantity]` only when the user explicitly asks about stock date or stock timing.
6. Do not describe `ProductPrice` as sales revenue; this model has no revenue measure.
7. Do not describe `ProductCost` as profit or margin; this model has no profit measure.
8. Prefer visible business attributes over hidden technical keys.
9. When a user says “sales” without specifying a metric, clarify whether they mean orders, quantity, line-item activity, or customers.
10. Use Product, Customer, Date, and Territory dimensions for grouping and filtering; dimensions filter `fact_sales` in one direction.

## Recommended AI Data Schema exposure

Expose the business-facing attributes and explicit measures, including:

- `fact_sales`: `OrderNumber`, `OrderQuantity`, and the eight explicit measures.
- `dim_customer`: visible customer attributes except `CustomerKey`.
- `dim_product`: visible product, classification, cost, and price attributes except `ProductKey`.
- `dim_date`: `Year`, `Month`, and `Day`; keep `DateKey` hidden.
- `dim_territory`: `Region`, `Country`, and `Continent`; keep `SalesTerritoryKey` hidden.

Keep technical relationship keys hidden from natural-language selection. Review whether personally identifying customer fields such as `EmailAddress` should be exposed in the Data Agent according to organizational privacy policy.
