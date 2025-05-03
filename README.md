## solution using powerbi DAX
![image](https://github.com/user-attachments/assets/a5dad2e0-bbd9-46d5-9db2-f02f3c66842a)




## 📊 Power BI DAX Concepts

This section summarizes key **DAX (Data Analysis Expressions)** concepts used in Power BI for creating custom calculations and enhancing data modeling.

---

### 🔹 What is DAX?

**DAX** is a formula language used in **Power BI**, **Power Pivot**, and **SSAS Tabular Models** to define custom calculations for **calculated columns**, **measures**, and **calculated tables**.

---

### 🔹 Filter Context

**Filter Context** refers to the **filters currently applied** to a calculation through visuals, slicers, page filters, etc.

📌 **Example**: In a "Total Sales by Region" visual, each region automatically applies a filter context to calculate total sales.

---

### 🔹 Measure

A **measure** is a formula that returns an **aggregated value**, calculated dynamically based on the current filter context.

```dax
Total Sales = SUM(Sales[Amount])
```

* Measures are evaluated on the **fly**.
* They are not stored in the data model.

---

### 🔹 Calculated Column

A **calculated column** is a **new column** added to a table using a DAX formula.

```dax
Sales Tax = Sales[Amount] * 0.18
```

* Computed during **data refresh**
* Stored in the data model
* Evaluated **row-by-row**

---

### 🔹 Difference: Measure vs Calculated Column

| Feature    | Measure                    | Calculated Column              |
| ---------- | -------------------------- | ------------------------------ |
| Evaluation | On-the-fly (at query time) | During data refresh            |
| Storage    | Not stored                 | Stored in model                |
| Context    | Filter context             | Row context                    |
| Use Case   | KPIs, Aggregated results   | Filtering, Relationships, etc. |

---

### 🔹 CALCULATE()

The `CALCULATE()` function **modifies the filter context** of an expression.

```dax
Sales West = CALCULATE([Total Sales], Region[Name] = "West")
```

---

### 🔹 ALL()

The `ALL()` function **removes filters** from a column or table.

```dax
Total Sales All Regions = CALCULATE([Total Sales], ALL(Region))
```

* `ALL(Column)` → removes filter from that column.
* `ALL(Table)` → removes all filters from the table.

---

### 🔹 ALLEXCEPT()

Keeps filters on specified columns and removes the rest.

```dax
Sales By Product = CALCULATE([Total Sales], ALLEXCEPT(Product, Product[Name]))
```

---

### 🔹 Direct Filter (Inline Filter)

You can directly apply filters inside `CALCULATE()` without using `FILTER()`:

```dax
High Sales = CALCULATE([Total Sales], Sales[Amount] > 1000)
```

---

### ✅ Summary Table

| Term               | Description                              |
| ------------------ | ---------------------------------------- |
| **DAX**            | Expression language for analytics        |
| **Filter Context** | Filters from visuals/slicers             |
| **Measure**        | Aggregated result, dynamic               |
| **Column**         | Static value per row                     |
| **CALCULATE()**    | Modifies filter context                  |
| **ALL()**          | Removes all filters                      |
| **ALLEXCEPT()**    | Removes all filters **except** specified |
| **Direct Filter**  | Inline filtering inside `CALCULATE()`    |

---

 📘 Tip

Use `CALCULATE()` whenever you want to:

 Override filters
 Add conditional logic to aggregations
Customize totals and KPIs

