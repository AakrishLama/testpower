# Power BI Project (PBIP) AI Agent Rules: Gold_semantic_model

## Scope & Purpose# Power BI Project (PBIP) AI Agent Rules: Gold_semantic_model

## Scope & Purpose
This ruleset governs AI assistant interactions within the `Gold_semantic_model` workspace, covering TMDL semantic models and `report.json` visual layouts.

---

## 1. Semantic Model Schema Reference (TMDL)
Tables are stored as individual `.tmdl` files under `definition/tables/`. Respect the existing schema structure:
* **`fact_sales`**: Transactional facts containing `OrderQuantity`, `OrderNumber`, `OrderLineItem`, and foreign keys.
* **`dim_product`**: Product catalog containing `CategoryName`, `ModelName`, `ProductName`, `ProductPrice`, `ProductColor`.
* **`dim_customer`**: Customer attributes including `FullName`, `EmailAddress`, `AnnualIncome`, `EducationLevel`.
* **`dim_date`**: Date dimensions including `DateKey`, `Year`, `Month`, `Day`.
* **`dim_territory`**: Geographic hierarchy containing `Continent`, `Country`, `Region`.

* **Descriptions:** Use triple slashes (`///`) directly above table or column definitions for descriptions.
* **Property Preservation:** Never delete or alter `lineageTag`, `sourceLineageTag`, or `dataType` properties unless explicitly instructed.
* **Measures:** Place custom DAX measures inside the appropriate table TMDL file.

---

## 2. Report Design & Visual Rules (`report.json`)
* **Layout Management:** Report pages and containers are structured inside `report.json`.
* **Data Role Binding:** When creating or fixing visuals (such as mapping `OrderQuantity` from `fact_sales` against `CategoryName` from `dim_product`), explicitly define data role projections (categories to category buckets, measures to value buckets) to avoid empty visual shells.
* **Schema Integrity:** Keep JSON modifications scoped strictly to visual configurations.

---

## 3. Execution Guidelines
* Validate all table and column references against the schema above before generating code or JSON edits.
* Keep modifications modular, clean, and targeted to the requested file path.# Power BI Project (PBIP) AI Agent Rules: Gold_semantic_model

## Scope & Purpose
This ruleset governs AI assistant interactions within the `Gold_semantic_model` workspace, covering TMDL semantic models and `report.json` visual layouts.

---

## 1. Semantic Model Schema Reference (TMDL)
Tables are stored as individual `.tmdl` files under `definition/tables/`. Respect the existing schema structure:
* **`fact_sales`**: Transactional facts containing `OrderQuantity`, `OrderNumber`, `OrderLineItem`, and foreign keys.
* **`dim_product`**: Product catalog containing `CategoryName`, `ModelName`, `ProductName`, `ProductPrice`, `ProductColor`.
* **`dim_customer`**: Customer attributes including `FullName`, `EmailAddress`, `AnnualIncome`, `EducationLevel`.
* **`dim_date`**: Date dimensions including `DateKey`, `Year`, `Month`, `Day`.
* **`dim_territory`**: Geographic hierarchy containing `Continent`, `Country`, `Region`.

* **Descriptions:** Use triple slashes (`///`) directly above table or column definitions for descriptions.
* **Property Preservation:** Never delete or alter `lineageTag`, `sourceLineageTag`, or `dataType` properties unless explicitly instructed.
* **Measures:** Place custom DAX measures inside the appropriate table TMDL file.

---

## 2. Report Design & Visual Rules (`report.json`)
* **Layout Management:** Report pages and containers are structured inside `report.json`.
* **Data Role Binding:** When creating or fixing visuals (such as mapping `OrderQuantity` from `fact_sales` against `CategoryName` from `dim_product`), explicitly define data role projections (categories to category buckets, measures to value buckets) to avoid empty visual shells.
* **Schema Integrity:** Keep JSON modifications scoped strictly to visual configurations.

---

## 3. Execution Guidelines
* Validate all table and column references against the schema above before generating code or JSON edits.
* Keep modifications modular, clean, and targeted to the requested file path.# Power BI Project (PBIP) AI Agent Rules: Gold_semantic_model

## Scope & Purpose
This ruleset governs AI assistant interactions within the `Gold_semantic_model` workspace, covering TMDL semantic models and `report.json` visual layouts.

---

## 1. Semantic Model Schema Reference (TMDL)
Tables are stored as individual `.tmdl` files under `definition/tables/`. Respect the existing schema structure:
* **`fact_sales`**: Transactional facts containing `OrderQuantity`, `OrderNumber`, `OrderLineItem`, and foreign keys.
* **`dim_product`**: Product catalog containing `CategoryName`, `ModelName`, `ProductName`, `ProductPrice`, `ProductColor`.
* **`dim_customer`**: Customer attributes including `FullName`, `EmailAddress`, `AnnualIncome`, `EducationLevel`.
* **`dim_date`**: Date dimensions including `DateKey`, `Year`, `Month`, `Day`.
* **`dim_territory`**: Geographic hierarchy containing `Continent`, `Country`, `Region`.

* **Descriptions:** Use triple slashes (`///`) directly above table or column definitions for descriptions.
* **Property Preservation:** Never delete or alter `lineageTag`, `sourceLineageTag`, or `dataType` properties unless explicitly instructed.
* **Measures:** Place custom DAX measures inside the appropriate table TMDL file.

---

## 2. Report Design & Visual Rules (`report.json`)
* **Layout Management:** Report pages and containers are structured inside `report.json`.
* **Data Role Binding:** When creating or fixing visuals (such as mapping `OrderQuantity` from `fact_sales` against `CategoryName` from `dim_product`), explicitly define data role projections (categories to category buckets, measures to value buckets) to avoid empty visual shells.
* **Schema Integrity:** Keep JSON modifications scoped strictly to visual configurations.

---

## 3. Execution Guidelines
* Validate all table and column references against the schema above before generating code or JSON edits.
* Keep modifications modular, clean, and targeted to the requested file path.# Power BI Project (PBIP) AI Agent Rules: Gold_semantic_model

## Scope & Purpose
This ruleset governs AI assistant interactions within the `Gold_semantic_model` workspace, covering TMDL semantic models and `report.json` visual layouts.

---

## 1. Semantic Model Schema Reference (TMDL)
Tables are stored as individual `.tmdl` files under `definition/tables/`. Respect the existing schema structure:
* **`fact_sales`**: Transactional facts containing `OrderQuantity`, `OrderNumber`, `OrderLineItem`, and foreign keys.
* **`dim_product`**: Product catalog containing `CategoryName`, `ModelName`, `ProductName`, `ProductPrice`, `ProductColor`.
* **`dim_customer`**: Customer attributes including `FullName`, `EmailAddress`, `AnnualIncome`, `EducationLevel`.
* **`dim_date`**: Date dimensions including `DateKey`, `Year`, `Month`, `Day`.
* **`dim_territory`**: Geographic hierarchy containing `Continent`, `Country`, `Region`.

* **Descriptions:** Use triple slashes (`///`) directly above table or column definitions for descriptions.
* **Property Preservation:** Never delete or alter `lineageTag`, `sourceLineageTag`, or `dataType` properties unless explicitly instructed.
* **Measures:** Place custom DAX measures inside the appropriate table TMDL file.

---

## 2. Report Design & Visual Rules (`report.json`)
* **Layout Management:** Report pages and containers are structured inside `report.json`.
* **Data Role Binding:** When creating or fixing visuals (such as mapping `OrderQuantity` from `fact_sales` against `CategoryName` from `dim_product`), explicitly define data role projections (categories to category buckets, measures to value buckets) to avoid empty visual shells.
* **Schema Integrity:** Keep JSON modifications scoped strictly to visual configurations.

---

## 3. Execution Guidelines
* Validate all table and column references against the schema above before generating code or JSON edits.
* Keep modifications modular, clean, and targeted to the requested file path.
This ruleset governs AI assistant interactions within the `Gold_semantic_model` workspace, covering TMDL semantic models and `report.json` visual layouts.

---

## 1. Semantic Model Schema Reference (TMDL)
Tables are stored as individual `.tmdl` files under `definition/tables/`. Respect the existing schema structure:
* **`fact_sales`**: Transactional facts containing `OrderQuantity`, `OrderNumber`, `OrderLineItem`, and foreign keys.
* **`dim_product`**: Product catalog containing `CategoryName`, `ModelName`, `ProductName`, `ProductPrice`, `ProductColor`.
* **`dim_customer`**: Customer attributes including `FullName`, `EmailAddress`, `AnnualIncome`, `EducationLevel`.
* **`dim_date`**: Date dimensions including `DateKey`, `Year`, `Month`, `Day`.
* **`dim_territory`**: Geographic hierarchy containing `Continent`, `Country`, `Region`.

* **Descriptions:** Use triple slashes (`///`) directly above table or column definitions for descriptions.
* **Property Preservation:** Never delete or alter `lineageTag`, `sourceLineageTag`, or `dataType` properties unless explicitly instructed.
* **Measures:** Place custom DAX measures inside the appropriate table TMDL file.

---

## 2. Report Design & Visual Rules (`report.json`)
* **Layout Management:** Report pages and containers are structured inside `report.json`.
* **Data Role Binding:** When creating or fixing visuals (such as mapping `OrderQuantity` from `fact_sales` against `CategoryName` from `dim_product`), explicitly define data role projections (categories to category buckets, measures to value buckets) to avoid empty visual shells.
* **Schema Integrity:** Keep JSON modifications scoped strictly to visual configurations.

---

## 3. Execution Guidelines
* Validate all table and column references against the schema above before generating code or JSON edits.
* Keep modifications modular, clean, and targeted to the requested file path.