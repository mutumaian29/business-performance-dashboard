# 🧮 DAX Measures Reference

Full documentation of all 15 DAX measures used in the Business Performance Dashboard.

---

## Revenue Measures

### YTD Total Revenue
```dax
YTD Total Revenue = 
TOTALYTD(
    SUM(FactSales[Revenue]),
    Date_Table[Date]
)
```
> Cumulative revenue from the start of the current year to the selected date context.

---

### MTD Revenue KPI
```dax
MTD Revenue KPI = 
TOTALMTD(
    SUM(FactSales[Revenue]),
    Date_Table[Date]
)
```
> Cumulative revenue from the start of the current month to the selected date.

---

### YoY Revenue Growth
```dax
YoY Revenue Growth = 
DIVIDE(
    [YTD Total Revenue] - CALCULATE([YTD Total Revenue], SAMEPERIODLASTYEAR(Date_Table[Date])),
    CALCULATE([YTD Total Revenue], SAMEPERIODLASTYEAR(Date_Table[Date])),
    0
)
```
> Percentage growth in YTD revenue compared to the same period last year.

---

### Total Revenue Difference
```dax
Total Revenue Difference = 
[YTD Total Revenue] - 
CALCULATE([YTD Total Revenue], SAMEPERIODLASTYEAR(Date_Table[Date]))
```
> Absolute revenue variance vs prior year same period.

---

### Revenue Difference Color
```dax
Revenue Difference Color = 
IF([Total Revenue Difference] >= 0, "Green", "Red")
```
> Dynamic color string used to conditionally format the Revenue Difference KPI card.

---

## Cost Measures

### YTD Total Cost
```dax
YTD Total Cost = 
TOTALYTD(
    SUM(FactSales[Cost]),
    Date_Table[Date]
)
```

---

### Total Cost Difference
```dax
Total Cost Difference = 
[YTD Total Cost] - 
CALCULATE([YTD Total Cost], SAMEPERIODLASTYEAR(Date_Table[Date]))
```

---

### Total Cost KPI
```dax
Total Cost KPI = 
TOTALMTD(
    SUM(FactSales[Cost]),
    Date_Table[Date]
)
```

---

### Cost Difference Color
```dax
Cost Difference Color = 
IF([Total Cost Difference] <= 0, "Green", "Red")
```
> Note: For cost, LOWER is better — so the color logic is inverted vs revenue.

---

### YoY Growth Cost
```dax
YoY Growth Cost = 
DIVIDE(
    [YTD Total Cost] - CALCULATE([YTD Total Cost], SAMEPERIODLASTYEAR(Date_Table[Date])),
    CALCULATE([YTD Total Cost], SAMEPERIODLASTYEAR(Date_Table[Date])),
    0
)
```

---

## Profit Measures

### YTD Profit
```dax
YTD Profit = 
TOTALYTD(
    SUM(FactSales[Revenue]) - SUM(FactSales[Cost]),
    Date_Table[Date]
)
```

---

### Total Profit Difference
```dax
Total Profit Difference = 
[YTD Profit] - 
CALCULATE([YTD Profit], SAMEPERIODLASTYEAR(Date_Table[Date]))
```

---

### Profit KPI
```dax
Profit KPI = 
TOTALMTD(
    SUM(FactSales[Revenue]) - SUM(FactSales[Cost]),
    Date_Table[Date]
)
```

---

### YoY Profit Growth
```dax
YoY Profit Growth = 
DIVIDE(
    [YTD Profit] - CALCULATE([YTD Profit], SAMEPERIODLASTYEAR(Date_Table[Date])),
    CALCULATE([YTD Profit], SAMEPERIODLASTYEAR(Date_Table[Date])),
    0
)
```

---

### Profit Difference Color
```dax
Profit Difference Color = 
IF([Total Profit Difference] >= 0, "Green", "Red")
```

---

## Notes

- All time intelligence measures require `Date_Table` to be marked as a **Date Table** in Power BI (Model view → right-click table → Mark as Date Table)
- Measures are stored in a dedicated measures table (shown as `f.` prefix in the data model) to keep the model organised
- `DIVIDE()` is used instead of `/` to safely handle division-by-zero scenarios
