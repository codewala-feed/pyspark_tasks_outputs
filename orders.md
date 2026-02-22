
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
