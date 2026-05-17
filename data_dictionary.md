# 📖 Data Dictionary

Column-level definitions for all tables in the Business Performance Dashboard data model.

---

## FactSales (Fact Table)

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `Order Quantity` | Number | Number of units ordered in a transaction | 5 |
| `Ship Date` | Date | Date the order was shipped / fulfilled | 2024-01-15 |
| `[Revenue/Sales]` | Decimal | Total revenue value of the transaction | 1,250.00 |
| `[Cost]` | Decimal | Total cost associated with the transaction | 875.00 |
| `[FK — Customer]` | Key | Foreign key linking to DimCustomer | — |
| `[FK — Product]` | Key | Foreign key linking to DimProducts | — |
| `[FK — Region]` | Key | Foreign key linking to DimRegion | — |
| `[FK — Date]` | Date | Foreign key linking to Date_Table | 2024-01-15 |

---

## DimCustomer (Customer Dimension)

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `Customer name` | Text | Full name of the customer or business | Acme Corp |
| `Channel` | Text | Sales channel through which the order was placed | Online, Retail, Wholesale |

---

## DimProducts (Product Dimension)

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `Product name` | Text | Name of the product or product line | Widget Pro X |

---

## DimRegion (Region Dimension)

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `Delivery Region Name` | Text | Geographic delivery region or territory | East Africa, Nairobi |
| `Channel` | Text | Regional channel classification | Direct, Partner |

---

## Date_Table (Date Dimension)

| Column | Data Type | Description | Example |
|--------|-----------|-------------|---------|
| `Date` | Date | Full date — primary key, marked as Date Table | 2024-01-15 |
| `Year` | Number | Calendar year | 2024 |
| `Quarter` | Text | Calendar quarter | Q1, Q2, Q3, Q4 |
| `Week Number` | Number | ISO week number within the year | 3 |
| `Month` | Text/Number | Month name or number | January / 1 |

> **Important:** `Date_Table[Date]` must be marked as the Date Table key in Power BI Model view for all time intelligence DAX functions (TOTALYTD, TOTALMTD, SAMEPERIODLASTYEAR) to work correctly.

---

## Relationships

| From Table | From Column | To Table | To Column | Cardinality |
|-----------|-------------|----------|-----------|-------------|
| FactSales | Ship Date | Date_Table | Date | Many → One |
| FactSales | [CustomerKey] | DimCustomer | [CustomerKey] | Many → One |
| FactSales | [ProductKey] | DimProducts | [ProductKey] | Many → One |
| FactSales | [RegionKey] | DimRegion | [RegionKey] | Many → One |

All relationships are **active** single-direction (dimension → fact) following standard star schema best practice.
