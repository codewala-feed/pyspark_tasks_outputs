
---

# 📊 Retail Orders – 50 PySpark Tasks with Expected Output

---

## Dataset Used

10 rows from `orders.csv`

---

# ✅ TRANSFORMATION TASKS

---

## 1. Rename `customer_name` → `name`

**Expected Columns:**

```
order_id, customer_id, name, gender, age, product, category,
quantity, price, order_date, city, payment_mode,
discount, delivery_days, rating
```

---

## 2. Rename `price` → `unit_price`

**Expected Columns:**

```
order_id, customer_id, customer_name, gender, age, product,
category, quantity, unit_price, order_date, city,
payment_mode, discount, delivery_days, rating
```

---

## 3. Add `total_amount = quantity * price`

| order_id | total_amount |
| -------- | ------------ |
| 1001     | 55000        |
| 1002     | 600          |
| 1003     | 60000        |
| 1004     | 40000        |
| 1005     | 30000        |
| 1006     | 2000         |
| 1007     | 3200         |
| 1008     | 45000        |
| 1009     | 5000         |
| 1010     | 12000        |

---

## 4. Add `final_amount = total_amount - discount`

| order_id | final_amount |
| -------- | ------------ |
| 1001     | 50000        |
| 1002     | 600          |
| 1003     | 58000        |
| 1004     | 37000        |
| 1005     | 29000        |
| 1006     | 1800         |
| 1007     | 3100         |
| 1008     | 40000        |
| 1009     | 4700         |
| 1010     | 10500        |

---

## 5. Add `tax = total_amount * 0.18`

| order_id | tax   |
| -------- | ----- |
| 1001     | 9900  |
| 1002     | 108   |
| 1003     | 10800 |
| 1004     | 7200  |
| 1005     | 5400  |
| 1006     | 360   |
| 1007     | 576   |
| 1008     | 8100  |
| 1009     | 900   |
| 1010     | 2160  |

---

## 6. Add `net_amount = final_amount + tax`

| order_id | net_amount |
| -------- | ---------- |
| 1001     | 59900      |
| 1002     | 708        |
| 1003     | 68800      |
| 1004     | 44200      |
| 1005     | 34400      |
| 1006     | 2160       |
| 1007     | 3676       |
| 1008     | 48100      |
| 1009     | 5600       |
| 1010     | 12660      |

---

## 7. Add `is_high_value` (total_amount > 50000)

True → 1001, 1003
False → Others

---

## 8. Add `age_group`

| Name   | Age | Group  |
| ------ | --- | ------ |
| Amit   | 25  | Adult  |
| Sneha  | 30  | Adult  |
| Rahul  | 35  | Adult  |
| Priya  | 28  | Adult  |
| John   | 40  | Senior |
| Anjali | 22  | Young  |
| Vikram | 29  | Adult  |
| Meena  | 33  | Adult  |
| Rohit  | 27  | Adult  |
| Kavya  | 31  | Adult  |

---

## 9. Extract `order_year`

All rows → 2023

---

## 10. Extract `order_month`

Values → 1 to 10

---

## 11. Extract `order_day`

Values → 15,10,5,12,18,22,19,25,10,5

---

# ✅ FILTER TASKS

---

## 12. Electronics category

Order IDs → 1001,1003,1006,1008,1010

---

## 13. City = Bangalore

Order IDs → 1001,1005,1010

---

## 14. total_amount > 30000

Order IDs → 1001,1003,1004,1008

---

## 15. Age between 25–35

All except 1005 (40) and 1006 (22)

---

## 16. payment_mode = UPI

1003,1006,1009

---

## 17. rating >= 4

1001,1002,1003,1005,1006,1007,1008,1010

---

## 18. quantity >= 2

1002,1003,1005,1007,1009

---

## 19. discount > 1000

1001,1003,1004,1008,1010

---

## 20. name starts with A

1001 (Amit), 1006 (Anjali)

---

## 21. name ends with 'a'

Sneha, Priya, Meena, Kavya

---

## 22. name contains 'h'

Sneha, Rahul, Rohit

---

# ✅ SORTING TASKS

---

## 23. Sort by total_amount desc (Top 5)

1003 (60000)
1001 (55000)
1008 (45000)
1004 (40000)
1005 (30000)

---

## 24. Sort by age asc

Anjali (22) lowest
John (40) highest

---

## 25. Top 5 highest total_amount

1003,1001,1008,1004,1005

---

## 26. Bottom 3 lowest rating

Rating = 3 → 1004,1009
Next lowest = 4 (any one)

---

# ✅ SELECTION TASK

---

## 27. Select name, product, total_amount

Example Row:

| name | product | total_amount |
| ---- | ------- | ------------ |
| Amit | Laptop  | 55000        |

---

# ✅ GROUP BY TASKS

---

## 28. Total sales per category

| Category      | Total  |
| ------------- | ------ |
| Electronics   | 174000 |
| Furniture     | 70000  |
| Fashion       | 8200   |
| Personal Care | 600    |

---

## 29. Avg rating per city

| City      | Avg Rating |
| --------- | ---------- |
| Bangalore | 4          |
| Delhi     | 4.5        |
| Mumbai    | 4.5        |
| Chennai   | 3          |
| Hyderabad | 5          |


---

# ✅ AGGREGATION TASKS

---

## 30. Count per `payment_mode`

| payment_mode | order_count |
| ------------ | ----------- |
| Card         | 4           |
| UPI          | 3           |
| Cash         | 2           |
| NetBanking   | 1           |

---

## 31. Average age per gender

| gender | avg_age |
| ------ | ------- |
| Male   | 31.2    |
| Female | 28.8    |

---

## 32. Max price per category

| category      | max_price |
| ------------- | --------- |
| Electronics   | 55000     |
| Furniture     | 40000     |
| Fashion       | 2500      |
| Personal Care | 200       |

---

## 33. Min price per category

| category      | min_price |
| ------------- | --------- |
| Electronics   | 2000      |
| Furniture     | 15000     |
| Fashion       | 800       |
| Personal Care | 200       |

---

## 34. Sum discount per city

| city      | total_discount |
| --------- | -------------- |
| Bangalore | 7500           |
| Delhi     | 100            |
| Mumbai    | 7000           |
| Chennai   | 3300           |
| Hyderabad | 200            |

---

## 35. Orders per month

| order_month | total_orders |
| ----------- | ------------ |
| 1           | 1            |
| 2           | 1            |
| 3           | 1            |
| 4           | 1            |
| 5           | 1            |
| 6           | 1            |
| 7           | 1            |
| 8           | 1            |
| 9           | 1            |
| 10          | 1            |

---

## 36. Count distinct customers

| metric             | value |
| ------------------ | ----- |
| distinct_customers | 10    |

---

## 37. Count distinct cities

| metric          | value |
| --------------- | ----- |
| distinct_cities | 5     |

---

## 38. Total revenue (sum of total_amount)

| metric        | total_revenue |
| ------------- | ------------- |
| total_revenue | 252800        |

---

## 39. Average delivery_days

| metric            | avg_delivery_days |
| ----------------- | ----------------- |
| avg_delivery_days | 4.1               |

---

## 40. Max delivery_days per city

| city      | max_delivery_days |
| --------- | ----------------- |
| Bangalore | 4                 |
| Delhi     | 6                 |
| Mumbai    | 5                 |
| Chennai   | 7                 |
| Hyderabad | 3                 |

---

# ✅ DERIVED COLUMN TASKS

---

## 41. delivery_status (Fast if <=3 else Slow)

| order_id | delivery_days | delivery_status |
| -------- | ------------- | --------------- |
| 1001     | 3             | Fast            |
| 1002     | 5             | Slow            |
| 1003     | 2             | Fast            |
| 1004     | 7             | Slow            |
| 1005     | 4             | Slow            |
| 1006     | 3             | Fast            |
| 1007     | 6             | Slow            |
| 1008     | 5             | Slow            |
| 1009     | 4             | Slow            |
| 1010     | 2             | Fast            |

---

## 42. high_rating (rating = 5)

| order_id | rating | high_rating |
| -------- | ------ | ----------- |
| 1001     | 4      | No          |
| 1002     | 5      | Yes         |
| 1003     | 4      | No          |
| 1004     | 3      | No          |
| 1005     | 4      | No          |
| 1006     | 5      | Yes         |
| 1007     | 4      | No          |
| 1008     | 5      | Yes         |
| 1009     | 3      | No          |
| 1010     | 4      | No          |

---

## 43. Replace null discount with 0

| order_id | discount                           |
| -------- | ---------------------------------- |
| All rows | No change (no null values present) |

---

## 44. Replace null rating with average rating

| order_id | rating                             |
| -------- | ---------------------------------- |
| All rows | No change (no null values present) |

---

## 45. Drop `customer_id`

**Expected Columns:**

| Columns After Drop |
| ------------------ |
| order_id           |
| customer_name      |
| gender             |
| age                |
| product            |
| category           |
| quantity           |
| price              |
| order_date         |
| city               |
| payment_mode       |
| discount           |
| delivery_days      |
| rating             |

---

## 46. Remove duplicate `order_id`

| metric                 | value |
| ---------------------- | ----- |
| total_rows_after_dedup | 10    |

---

## 47. Convert name to uppercase

| original_name | uppercase_name |
| ------------- | -------------- |
| Amit          | AMIT           |
| Sneha         | SNEHA          |
| Rahul         | RAHUL          |
| Priya         | PRIYA          |
| John          | JOHN           |
| Anjali        | ANJALI         |
| Vikram        | VIKRAM         |
| Meena         | MEENA          |
| Rohit         | ROHIT          |
| Kavya         | KAVYA          |

---

## 48. Convert product to lowercase

| original_product | lowercase_product |
| ---------------- | ----------------- |
| Laptop           | laptop            |
| Shampoo          | shampoo           |
| Mobile           | mobile            |
| Sofa             | sofa              |
| Table            | table             |
| Headphones       | headphones        |
| T-shirt          | t-shirt           |
| Refrigerator     | refrigerator      |
| Shoes            | shoes             |
| Microwave        | microwave         |

---

## 49. price_category

(Low <5000, Medium 5000–30000, High >30000)

| order_id | price | price_category |
| -------- | ----- | -------------- |
| 1001     | 55000 | High           |
| 1002     | 200   | Low            |
| 1003     | 30000 | Medium         |
| 1004     | 40000 | High           |
| 1005     | 15000 | Medium         |
| 1006     | 2000  | Low            |
| 1007     | 800   | Low            |
| 1008     | 45000 | High           |
| 1009     | 2500  | Low            |
| 1010     | 12000 | Medium         |

---

## 50. Second highest total_amount (Window Function)

| rank | order_id | total_amount |
| ---- | -------- | ------------ |
| 1    | 1003     | 60000        |
| 2    | 1001     | 55000        |

---

# Window function tasks sample outputs 
---

## ✅ 1️⃣ row_number() partitioned by city ordered by price DESC

| order_id | city      | price | row_number |
| -------- | --------- | ----- | ---------- |
| 1001     | Bangalore | 55000 | 1          |
| 1005     | Bangalore | 15000 | 2          |
| 1010     | Bangalore | 12000 | 3          |
| 1015     | Bangalore | 5000  | 4          |
| 1020     | Bangalore | 2000  | 5          |

⚠ Showing only 5 rows from output

---

## ✅ 2️⃣ rank() partitioned by category ordered by price DESC

| order_id | category    | price | rank |
| -------- | ----------- | ----- | ---- |
| 1011     | Electronics | 60000 | 1    |
| 1001     | Electronics | 55000 | 2    |
| 1008     | Electronics | 45000 | 3    |
| 1019     | Electronics | 42000 | 4    |
| 1013     | Electronics | 38000 | 5    |

⚠ Showing only 5 rows from output

---

## ✅ 3️⃣ dense_rank() partitioned by city ordered by rating DESC

| order_id | city      | rating | dense_rank |
| -------- | --------- | ------ | ---------- |
| 1001     | Bangalore | 4      | 1          |
| 1005     | Bangalore | 4      | 1          |
| 1010     | Bangalore | 4      | 1          |
| 1015     | Bangalore | 4      | 1          |
| 1020     | Bangalore | 3      | 2          |

⚠ Showing only 5 rows from output

---

## ✅ 4️⃣ Top 2 Highest Priced Products per Category

| category    | order_id | price |
| ----------- | -------- | ----- |
| Electronics | 1011     | 60000 |
| Electronics | 1001     | 55000 |
| Furniture   | 1014     | 50000 |
| Furniture   | 1004     | 40000 |
| Fashion     | 1015     | 5000  |

⚠ Showing only 5 rows from output

---

## ✅ 5️⃣ Lowest Rated Order per City

| city      | order_id | rating |
| --------- | -------- | ------ |
| Bangalore | 1020     | 3      |
| Chennai   | 1004     | 3      |
| Delhi     | 1007     | 4      |
| Hyderabad | 1006     | 5      |
| Mumbai    | 1003     | 4      |

⚠ Showing only 5 rows from output

---

## ✅ 6️⃣ Running Total of Price (Example: Bangalore)

| order_id | order_date | price | running_total |
| -------- | ---------- | ----- | ------------- |
| 1001     | 2023-01-15 | 55000 | 55000         |
| 1005     | 2023-05-18 | 15000 | 70000         |
| 1015     | 2023-03-18 | 5000  | 75000         |
| 1020     | 2023-08-12 | 2000  | 77000         |
| 1010     | 2023-10-05 | 12000 | 89000         |

⚠ Showing only 5 rows from output

---

## ✅ 7️⃣ Cumulative Quantity per Category (Electronics)

| order_id | quantity | cumulative_qty |
| -------- | -------- | -------------- |
| 1001     | 1        | 1              |
| 1003     | 2        | 3              |
| 1006     | 1        | 4              |
| 1008     | 1        | 5              |
| 1010     | 1        | 6              |

⚠ Showing only 5 rows from output

---

## ✅ 8️⃣ Average Price per Category (Window)

| order_id | category    | price | avg_price_category |
| -------- | ----------- | ----- | ------------------ |
| 1001     | Electronics | 55000 | 33900              |
| 1003     | Electronics | 30000 | 33900              |
| 1006     | Electronics | 2000  | 33900              |
| 1008     | Electronics | 45000 | 33900              |
| 1010     | Electronics | 12000 | 33900              |

⚠ Showing only 5 rows from output

---

## ✅ 9️⃣ Total Revenue per City (Window)

| order_id | city      | price | total_city_price |
| -------- | --------- | ----- | ---------------- |
| 1001     | Bangalore | 55000 | 89000            |
| 1005     | Bangalore | 15000 | 89000            |
| 1010     | Bangalore | 12000 | 89000            |
| 1015     | Bangalore | 5000  | 89000            |
| 1020     | Bangalore | 2000  | 89000            |

⚠ Showing only 5 rows from output

---

## ✅ 🔟 % Contribution to City Revenue

| order_id | city      | price | % contribution |
| -------- | --------- | ----- | -------------- |
| 1001     | Bangalore | 55000 | 61.79%         |
| 1005     | Bangalore | 15000 | 16.85%         |
| 1010     | Bangalore | 12000 | 13.48%         |
| 1015     | Bangalore | 5000  | 5.61%          |
| 1020     | Bangalore | 2000  | 2.24%          |

⚠ Showing only 5 rows from output

---

## ✅ 1️⃣1️⃣ Lag Price Difference (Mumbai)

| order_id | price | prev_price | diff   |
| -------- | ----- | ---------- | ------ |
| 1003     | 30000 | null       | null   |
| 1008     | 45000 | 30000      | 15000  |
| 1017     | 7000  | 45000      | -38000 |
| 1012     | 3500  | 7000       | -3500  |
| —        | —     | —          | —      |

⚠ Showing only 5 rows from output

---

## ✅ 1️⃣2️⃣ Lead Price (Electronics)

| order_id | price | next_price |
| -------- | ----- | ---------- |
| 1001     | 55000 | 30000      |
| 1003     | 30000 | 2000       |
| 1006     | 2000  | 45000      |
| 1008     | 45000 | 12000      |
| 1010     | 12000 | 60000      |

⚠ Showing only 5 rows from output

---

## ✅ 1️⃣3️⃣ Delivery Day Difference (Delhi)

| order_id | delivery_days | prev_delivery | diff |
| -------- | ------------- | ------------- | ---- |
| 1002     | 5             | null          | null |
| 1007     | 6             | 5             | 1    |
| 1011     | 3             | 6             | -3   |
| 1016     | 4             | 3             | 1    |
| —        | —             | —             | —    |

⚠ Showing only 5 rows from output

---

## ✅ 1️⃣4️⃣ Second Highest Price per Category

| category      | second_highest_price |
| ------------- | -------------------- |
| Electronics   | 55000                |
| Furniture     | 42000                |
| Fashion       | 3500                 |
| Personal Care | null                 |
| —             | —                    |

⚠ Showing only 5 rows from output

---

## ✅ 1️⃣5️⃣ Moving Average (Last 3 Orders Overall)

| order_id | price | moving_avg_3 |
| -------- | ----- | ------------ |
| 1001     | 55000 | 55000        |
| 1002     | 200   | 27600        |
| 1003     | 30000 | 28400        |
| 1004     | 40000 | 23400        |
| 1005     | 15000 | 28333        |

⚠ Showing only 5 rows from output

---
