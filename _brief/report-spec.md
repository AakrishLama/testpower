# Report Spec

## Report identity
- Report name: Sales Performance Executive Report
- Semantic model: `scratch_from_warehouse\scratch_model.SemanticModel`
- Audience: Executives / leadership
- Primary purpose: Track sales performance over time and identify the product, customer, and territory drivers behind the result.
- Delivery target: Local PBIP first

## User decisions and constraints
- Scope: Two-page report using the existing Direct Lake sales star schema.
- Page count: 2
- Interactivity: One synchronized Year slicer; page 2 adds Territory, Country, and Category filters. Cross-filtering remains enabled where it clarifies drivers.
- Design direction: Minimal restrained — white/off-white surface, slate text, one blue accent, strong hierarchy, no chartjunk.
- Publishing: Not requested; keep all changes local.
- Tooling: Use the report authoring workflow for PBIR/PBIP and the semantic-model authoring workflow for measures.
- Model edit permissions: Measures may be added to the local semantic model after approval; existing relationships remain unchanged.
- Accessibility: WCAG AA contrast, insight-driven alt text, logical tab order, keyboard-reachable slicers, and redundant labels for color-coded changes.
- Data caveats: The model currently has no explicit measures. The active date role is `OrderDateKey`; `StockDateKey` is inactive and should not drive the executive page unless a dedicated stock-date measure is added.

## Narrative
- Core story: Sales volume is changing over time; the report first states the current performance, then exposes which products, territories, customers, and categories explain it.
- Audience promise: In one scan, leadership can see the scale and trajectory of sales, then move directly to the strongest and weakest contributors.
- Key questions answered:
  - How many orders and line items are being processed?
  - How has order quantity changed over time?
  - Which products and categories contribute most?
  - Which territories and countries lead or lag?
  - Which customers account for the largest order volume?

## Design identity (from the design mode)
- Tone: Minimal Restrained
- Signature: Composite KPI focus — each primary KPI combines an absolute value with a period context label, while the explanatory trend or ranking visual remains the dominant region.
- Brownfield delta: Not applicable; this is a blank local report shell.

## Page plan
1. Sales performance at a glance
   - Archetype: Executive Summary
   - Layout variant (A): Hero-Right — four concise KPIs support a single order-quantity trend, with ranked drivers beneath.
   - Purpose: Give leadership a sub-10-second view of current order volume, quantity, line-item activity, and customer reach, then show the main time trend.
   - Visuals:
     - Descriptive title textbox: “Order volume and quantity show the current sales trajectory”
     - Year dropdown slicer
     - KPI cards: Total Orders, Total Order Quantity, Total Line Items, Active Customers
     - Line chart: Total Order Quantity by DateKey, with Year context
     - Sorted horizontal bar: Total Order Quantity by CategoryName
     - Sorted horizontal bar: Total Order Quantity by Country
     - Compact footer textbox with source/model and active filter context
   - Fields/measures: `fact_sales[OrderNumber]`, `fact_sales[OrderQuantity]`, `fact_sales[OrderLineItem]`, `dim_customer[CustomerKey]`, `dim_date[DateKey]`, `dim_date[Year]`, `dim_product[CategoryName]`, `dim_territory[Country]`.
   - Slicers/interactions: Year is synchronized to page 2. Clicking a category or country cross-filters the trend and KPI cards. No more than one visible slicer.

2. Drivers by product, territory, and customer
   - Archetype: Analytical Canvas
   - Layout variant (B): Inline-Slicers — three focused slicers fit the title band, leaving the full-width analytical area for trend, ranking, and detail.
   - Purpose: Explain the executive page's result by comparing product categories, territories, countries, and top customers under the selected context.
   - Visuals:
     - Descriptive title textbox: “Product and geography explain where order quantity is concentrated”
     - Slicers: Year, Country, CategoryName
     - Full-width line chart: Total Order Quantity by DateKey
     - Sorted horizontal bar: Top 10 ProductName by Total Order Quantity
     - Sorted horizontal bar: SalesTerritory Region by Total Order Quantity
     - Detail table: Top customers with FullName, Total Orders, Total Order Quantity, and Last Order Date
   - Fields/measures: `dim_date[DateKey]`, `dim_date[Year]`, `dim_product[ProductName]`, `dim_product[CategoryName]`, `dim_territory[Region]`, `dim_territory[Country]`, `dim_customer[FullName]`, `fact_sales[OrderNumber]`, `fact_sales[OrderQuantity]`.
   - Slicers/interactions: Year syncs with page 1. Country and CategoryName are page-specific. Selecting a bar filters the customer table and trend; the table remains sortable and limited to the top 10 customers by quantity.

## Design system summary
- Theme name + base palette: `Minimal Restrained Sales`; near-white page surface `#F8FAFC`, slate foreground `#0F172A`, one primary blue accent `#2563EB`, supporting greys `#64748B`, `#CBD5E1`, and `#E2E8F0`. Preserve the base theme's type-specific PBIR safeguards.
- Color semantics: Blue represents the primary order-quantity measure across charts and KPI emphasis; neutral greys represent context. Do not use color alone for positive/negative interpretation; use labels and direction text.
- Typography pairing: Segoe UI Semibold for titles and visual headers, Segoe UI regular for body labels, with tabular-looking numeric formatting where supported.
- Layout pattern: FHD 1920x1080, 12-column grid, 32px margins, 24px gutters, 8px snap, 24px inter-group spacing.
- Accessibility commitments: Explicit alt text for every non-decorative visual, 4.5:1 body-text contrast, 3:1 non-text contrast, visible slicer state, and tab order from title to filters to visuals left-to-right and top-to-bottom.

## Model requirements
- Existing measures: None.
- New measures:
  - `Total Orders = DISTINCTCOUNT('fact_sales'[OrderNumber])`
  - `Total Order Quantity = SUM('fact_sales'[OrderQuantity])`
  - `Total Line Items = SUM('fact_sales'[OrderLineItem])`
  - `Active Customers = DISTINCTCOUNT('fact_sales'[CustomerKey])`
  - `Last Order Date = MAX('fact_sales'[OrderDateKey])`
  - `Stock Date Order Quantity = CALCULATE([Total Order Quantity], USERELATIONSHIP('fact_sales'[StockDateKey], 'dim_date'[DateKey]))` (for future stock-date analysis; not required on page 1)
- New calculated columns: None.
- Relationship/sort requirements: Keep the five existing star-schema relationships. Keep `OrderDateKey` active and `StockDateKey` inactive. Use `dim_date[DateKey]` as the continuous trend axis; use numeric `dim_date[Month]` only if a month-level visual is later added. Hide technical keys as already configured.

## Canonical design contract

```yaml
Design Brief:
  generated_by: powerbi-report-cli
  contract_version: 1
  mode: greenfield
  design_identity:
    tone: Minimal Restrained
    signature: Composite KPI focus — every primary KPI pairs an absolute value with context while trend and ranking visuals carry the explanatory weight.
  theme:
    name: Minimal Restrained Sales
    page_surface: "#F8FAFC"
    foreground: "#0F172A"
    accent: "#2563EB"
    muted: "#64748B"
    baseline: "#E2E8F0"
    typography:
      title: "Segoe UI Semibold"
      body: "Segoe UI"
    safeguards: Preserve base.json textbox, cardVisual, table, hidden-header, and chart defaults.
  color_map:
    Total Orders: "#2563EB"
    Total Order Quantity: "#2563EB"
    Total Line Items: "#64748B"
    Active Customers: "#0F172A"
  pages:
    - name: Sales performance at a glance
      role: landing
      archetype: Executive Summary
      layout_variant: A
      variant_rationale: Four concise KPIs and one meaningful order-quantity trend make the Hero-Right composition the fastest executive scan.
      layout_contract:
        canvas: { width: 1920, height: 1080, margin: 32, gutter: 24, snap: 8 }
        grid:
          columns: 12
          rows: 12
          regions:
            header: [1, 1, 9, 2]
            filters: [9, 1, 13, 2]
            kpis: [1, 3, 9, 5]
            hero: [9, 3, 13, 7]
            drivers: [1, 8, 7, 12]
            geography: [7, 8, 13, 12]
            footer: [1, 12, 13, 13]
        placements:
          - id: page_title
            region: header
            kind: textbox
            text: Order volume and quantity show the current sales trajectory
            purpose: State the executive takeaway before the reader interprets visuals.
          - id: year_slicer
            region: filters
            kind: slicer
            purpose: Set the shared reporting year.
            field_bindings: ["dim_date[Year]"]
          - id: total_orders_card
            region: kpis
            kind: cardVisual
            purpose: Show the number of distinct orders with period context.
            field_bindings: ["[Total Orders]"]
          - id: total_quantity_card
            region: kpis
            kind: cardVisual
            purpose: Show total units ordered with period context.
            field_bindings: ["[Total Order Quantity]"]
          - id: total_line_items_card
            region: kpis
            kind: cardVisual
            purpose: Show line-item activity with period context.
            field_bindings: ["[Total Line Items]"]
          - id: active_customers_card
            region: kpis
            kind: cardVisual
            purpose: Show customer reach with period context.
            field_bindings: ["[Active Customers]"]
          - id: quantity_trend
            region: hero
            kind: lineChart
            purpose: Explain whether order quantity is rising, falling, or stable over time.
            field_bindings: ["dim_date[DateKey]", "[Total Order Quantity]"]
          - id: category_driver
            region: drivers
            kind: barChart
            purpose: Rank product categories by order quantity.
            field_bindings: ["dim_product[CategoryName]", "[Total Order Quantity]"]
          - id: country_driver
            region: geography
            kind: barChart
            purpose: Rank countries by order quantity.
            field_bindings: ["dim_territory[Country]", "[Total Order Quantity]"]
          - id: report_footer
            region: footer
            kind: textbox
            text: Direct Lake warehouse model · Order date context · Select a bar to filter the page
            purpose: Provide source and interaction context.
        space_audit:
          content_cell_count: 108
          placed_cell_count: 96
          empty_cell_pct: 11
          unplaced_regions: []
          largest_region: { name: hero, pct_of_content: 22 }
          balance_rationale: The trend is the largest explanatory visual; KPI cards are compact and drivers occupy balanced lower-page regions.
    - name: Drivers by product, territory, and customer
      role: detail
      archetype: Analytical Canvas
      layout_variant: B
      variant_rationale: Three slicers are sufficient for focused exploration, so inline controls preserve the full-width hero and detail area.
      layout_contract:
        canvas: { width: 1920, height: 1080, margin: 32, gutter: 24, snap: 8 }
        grid:
          columns: 12
          rows: 12
          regions:
            header: [1, 1, 9, 2]
            filters: [9, 1, 13, 2]
            hero: [1, 3, 13, 6]
            products: [1, 6, 5, 10]
            territories: [5, 6, 9, 10]
            customers: [9, 6, 13, 12]
            footer: [1, 12, 13, 13]
        placements:
          - id: page_title
            region: header
            kind: textbox
            text: Product and geography explain where order quantity is concentrated
            purpose: State the analytical question for the page.
          - id: year_slicer
            region: filters
            kind: slicer
            purpose: Preserve the shared year context.
            field_bindings: ["dim_date[Year]"]
          - id: country_slicer
            region: filters
            kind: slicer
            purpose: Focus the analysis on a country.
            field_bindings: ["dim_territory[Country]"]
          - id: category_slicer
            region: filters
            kind: slicer
            purpose: Focus the analysis on a product category.
            field_bindings: ["dim_product[CategoryName]"]
          - id: detail_quantity_trend
            region: hero
            kind: lineChart
            purpose: Show the selected-context order quantity trend.
            field_bindings: ["dim_date[DateKey]", "[Total Order Quantity]"]
          - id: top_products
            region: products
            kind: barChart
            purpose: Rank the top 10 products by order quantity.
            field_bindings: ["dim_product[ProductName]", "[Total Order Quantity]"]
          - id: territory_ranking
            region: territories
            kind: barChart
            purpose: Compare sales territories by order quantity.
            field_bindings: ["dim_territory[Region]", "[Total Order Quantity]"]
          - id: customer_detail
            region: customers
            kind: tableEx
            purpose: Provide precise top-customer detail for follow-up.
            field_bindings: ["dim_customer[FullName]", "[Total Orders]", "[Total Order Quantity]", "[Last Order Date]"]
          - id: report_footer
            region: footer
            kind: textbox
            text: Use the slicers and bar selections to explain the current sales result
            purpose: Make filter state and intended interaction explicit.
        space_audit:
          content_cell_count: 108
          placed_cell_count: 101
          empty_cell_pct: 6
          unplaced_regions: []
          largest_region: { name: hero, pct_of_content: 25 }
          balance_rationale: The full-width trend establishes context; product, territory, and customer views share the lower area without allowing the detail table to dominate.
```

## Implementation notes
- Model changes: Add the listed explicit measures with display names, descriptions, and format strings. Hide or set `summarizeBy: none` on any base columns exposed only through measures where applicable.
- PBIR/report authoring: Create two pages in the existing local report, register the minimal restrained theme, use insight-driven titles and alt text, hide visual headers where appropriate, and preserve the reserved title/filter band.
- Validation: Validate the report definition after each logical authoring batch. Verify all coordinates are on the 8px grid, no visuals overlap, bar charts sort descending, and slicers use the intended fields.
- Desktop screenshot verification: Reload Power BI Desktop if available and review both pages for clipping, contrast, readable labels, and scan hierarchy.
- Publishing boundary: Do not publish to Fabric in this phase.
- Risks: `dim_date` lacks a month-name column and the model has no existing measures; trend granularity and executive period-over-period deltas may require additional measures or a later date-attribute enhancement.
