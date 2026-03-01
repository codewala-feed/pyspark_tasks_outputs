---

# 📘 Window Functions – Definitions

## 🔹 What is a Window Function?

A **window function** performs calculations across a set of rows that are related to the current row, while **retaining all original rows** in the result.

Unlike `groupBy`, window functions do not collapse rows.
They allow aggregation, ranking, and comparison at a row level.

---

## 🔹 What is a Window?

A **window** is a logical subset of rows defined relative to the current row using:

* `partitionBy()` → divides data into groups
* `orderBy()` → defines order inside each group
* `rowsBetween()` → defines frame boundaries

---

## 🔹 partitionBy()

`partitionBy()` divides data into logical groups (partitions) similar to `groupBy`,
but **does not collapse rows**.

Each calculation is performed independently within each partition.

Example meaning:

> “For each city, calculate something.”

---

## 🔹 orderBy() (in Window)

Defines the order of rows inside each partition.

This is required for:

* Running totals
* Ranking
* lead() / lag()
* Cumulative calculations

---

## 🔹 rowsBetween()

Defines the range of rows used in calculation relative to the current row.

Common usage:

* `unboundedPreceding → currentRow` → Running total
* `-1, 1` → Moving window
* `currentRow → unboundedFollowing` → Forward accumulation

---

# 📊 groupBy vs Window (Core Concept)

## 🔹 groupBy()

* Aggregates data
* Collapses rows
* Returns one row per group
* Used for summary reports

Definition:

> `groupBy()` is used to aggregate data and reduce the number of rows by grouping records based on specified columns.

---

## 🔹 Window (partitionBy)

* Performs calculations over related rows
* Does NOT collapse rows
* Keeps original row-level detail
* Used for advanced analytics

Definition:

> A window function with `partitionBy()` performs calculations across grouped data while preserving each original row in the output.

---

# 🏆 Ranking Functions

## 🔹 row_number()

Assigns a unique sequential number to each row within a partition based on ordering.
No gaps, no ties.

---

## 🔹 rank()

Assigns the same rank to tied values, but leaves gaps in ranking sequence.

---

## 🔹 dense_rank()

Assigns the same rank to tied values, without gaps in ranking sequence.

---

# 🔄 Lead and Lag

## 🔹 lag()

Accesses data from a previous row within the same partition.

Used for:

* Comparing with previous record
* Calculating differences
* Trend analysis

---

## 🔹 lead()

Accesses data from the next row within the same partition.

Used for:

* Forecast comparison
* Next event analysis

---

# 📈 Aggregation Over Window

Common window aggregations:

* `sum()` → Running total
* `avg()` → Moving average
* `count()` → Running count
* `max()` / `min()` → Highest/lowest in partition

Definition:

> Window aggregation allows applying aggregate functions over partitions while retaining individual rows.

---


# WINDOW FUNCTIONS & groupBy() vs partitionBy()
---

# 🎯 Real-World Scenario: E-Commerce Orders

Imagine you work as a Data Engineer in an e-commerce company.

Your manager asks:

1. “What is total sales per city?”
2. “For each order, what percentage does it contribute to its city’s total sales?”
3. “Show running sales growth in each city over time.”

We will solve all three.

---

# 📦 Dataset: Orders Table

| order_id | city   | order_date | amount |
| -------- | ------ | ---------- | ------ |
| 1        | Delhi  | 2024-01-01 | 100    |
| 2        | Delhi  | 2024-01-02 | 200    |
| 3        | Delhi  | 2024-01-03 | 300    |
| 4        | Mumbai | 2024-01-01 | 400    |
| 5        | Mumbai | 2024-01-02 | 500    |

---

# 🔥 CASE 1: Total Sales Per City

Manager wants summary report.

This is a **reporting question**.

### ✅ Use groupBy()

```python
df.groupBy("city").sum("amount")
```

### Output:

| city   | total_sales |
| ------ | ----------- |
| Delhi  | 600         |
| Mumbai | 900         |

### Why groupBy is correct here?

* We only need summary.
* We don’t care about individual orders.
* Rows are collapsed.

👉 groupBy = final aggregated report.

---

# 🔥 CASE 2: Percentage Contribution of Each Order to City Sales

Manager now asks:

> “For every order, show what % it contributes to its city’s total sales.”

Now this is different.

We need:

* City total
* AND individual order
* In the SAME row

If we use groupBy, we lose individual rows.

So we use **Window function (partitionBy)**.

---

## Step 1: Define Window

```python
from pyspark.sql.window import Window
from pyspark.sql.functions import sum, col

windowSpec = Window.partitionBy("city")
```

---

## Step 2: Add City Total Without Collapsing

```python
df.withColumn("city_total",
              sum("amount").over(windowSpec))
```

### Output:

| order_id | city   | amount | city_total |
| -------- | ------ | ------ | ---------- |
| 1        | Delhi  | 100    | 600        |
| 2        | Delhi  | 200    | 600        |
| 3        | Delhi  | 300    | 600        |
| 4        | Mumbai | 400    | 900        |
| 5        | Mumbai | 500    | 900        |

---

### ❓ Why repeating 600 makes sense?

Because now we can compute percentage per order:

```python
.withColumn("percentage",
            col("amount")/col("city_total") * 100)
```

### Final Output:

| order_id | city   | amount | city_total | percentage |
| -------- | ------ | ------ | ---------- | ---------- |
| 1        | Delhi  | 100    | 600        | 16.67%     |
| 2        | Delhi  | 200    | 600        | 33.33%     |
| 3        | Delhi  | 300    | 600        | 50%        |
| 4        | Mumbai | 400    | 900        | 44.44%     |
| 5        | Mumbai | 500    | 900        | 55.56%     |

---

### 🚀 Now it makes business sense:

We can see:

* Which order contributes most
* Sales distribution
* High value transactions

This is IMPOSSIBLE with groupBy alone.

---

# 🔥 CASE 3: Running Sales Growth Per City

Manager asks:

> “Show cumulative sales growth in each city over time.”

Now we need:

* Partition by city
* Order by date
* Running sum

---

## Step 1: Define Window

```python
windowSpec = Window.partitionBy("city") \
                   .orderBy("order_date") \
                   .rowsBetween(Window.unboundedPreceding,
                                Window.currentRow)
```

---

## Step 2: Running Total

```python
df.withColumn("running_sales",
              sum("amount").over(windowSpec))
```

---

### Step-by-Step Calculation (Delhi)

Orders sorted by date:

| date  | amount |
| ----- | ------ |
| Jan 1 | 100    |
| Jan 2 | 200    |
| Jan 3 | 300    |

Running calculation:

Row 1 → 100
Row 2 → 100 + 200 = 300
Row 3 → 100 + 200 + 300 = 600

---

### Final Output:

| order_id | city   | amount | running_sales |
| -------- | ------ | ------ | ------------- |
| 1        | Delhi  | 100    | 100           |
| 2        | Delhi  | 200    | 300           |
| 3        | Delhi  | 300    | 600           |
| 4        | Mumbai | 400    | 400           |
| 5        | Mumbai | 500    | 900           |

---

### 🚀 Business Usage

This is used for:

* Sales dashboards
* Growth analysis
* Daily revenue trends
* KPI tracking

---

# 🔴 CLEAR DIFFERENCE: groupBy vs partitionBy

| Scenario                | Use groupBy | Use Window (partitionBy) |
| ----------------------- | ----------- | ------------------------ |
| Final summary report    | ✅ Yes       | ❌ No                     |
| Need row-level detail   | ❌ No        | ✅ Yes                    |
| Percentage contribution | ❌ No        | ✅ Yes                    |
| Running total           | ❌ No        | ✅ Yes                    |
| Ranking top products    | ❌ No        | ✅ Yes                    |

---

# 🧠 How To Think About It

### groupBy

> “I don’t need original rows anymore.”

### Window

> “I need original rows + aggregated insight.”

---

# 💡 Real Interview Explanation

If interviewer asks:

**Why not use groupBy instead of window?**

You answer:

> groupBy collapses rows and gives aggregated result.
> Window functions allow aggregation while retaining row-level detail, enabling calculations like percentage contribution, running totals, ranking, and comparisons.

That’s a strong answer.

---

If you want next, I can explain:

* Ranking with real HR salary scenario
* lag/lead with delivery tracking example
* Advanced window frames (sliding windows)
* Trick interview questions

Just tell me.
