tasks using **pure Python only** (no pandas, no SQL, no external libraries — only built-in modules like `datetime`, `math`, etc.).

---

# ✅ Sample Data (List of Dictionaries)

We’ll assume your dataset looks like this:

```python
from datetime import datetime
from statistics import mean

orders = [
    {
        "order_id": 1,
        "customer_id": 101,
        "customer_name": "Akhil",
        "age": 28,
        "gender": "Male",
        "product": "Laptop",
        "category": "Electronics",
        "price": 60000,
        "quantity": 1,
        "discount": 2000,
        "city": "Bangalore",
        "rating": 5,
        "payment_mode": "UPI",
        "delivery_days": 2,
        "order_date": "2024-01-15"
    },
    {
        "order_id": 2,
        "customer_id": 102,
        "customer_name": "Sneha",
        "age": 22,
        "gender": "Female",
        "product": "Mobile",
        "category": "Electronics",
        "price": 20000,
        "quantity": 2,
        "discount": None,
        "city": "Mumbai",
        "rating": 4,
        "payment_mode": "Card",
        "delivery_days": 5,
        "order_date": "2024-02-10"
    }
]
```

---

# 🔹 1. Rename Columns

```python
for order in orders:
    order["name"] = order.pop("customer_name")
    order["unit_price"] = order.pop("price")
```

---

# 🔹 2. Add Derived Columns

```python
for order in orders:
    order["discount"] = order["discount"] or 0  # Replace null discount
    
    order["total_amount"] = order["quantity"] * order["unit_price"]
    order["final_amount"] = order["total_amount"] - order["discount"]
    order["tax"] = order["total_amount"] * 0.18
    order["net_amount"] = order["final_amount"] + order["tax"]
    order["is_high_value"] = order["total_amount"] > 50000
```

---

# 🔹 3. Age Group Column

```python
for order in orders:
    age = order["age"]
    if age < 25:
        order["age_group"] = "Young"
    elif 25 <= age <= 35:
        order["age_group"] = "Adult"
    else:
        order["age_group"] = "Senior"
```

---

# 🔹 4. Extract Year, Month, Day

```python
for order in orders:
    dt = datetime.strptime(order["order_date"], "%Y-%m-%d")
    order["order_year"] = dt.year
    order["order_month"] = dt.month
    order["order_day"] = dt.day
```

---

# 🔹 5. Filtering Examples

```python
electronics = [o for o in orders if o["category"] == "Electronics"]

bangalore_orders = [o for o in orders if o["city"] == "Bangalore"]

high_value = [o for o in orders if o["total_amount"] > 30000]

age_25_35 = [o for o in orders if 25 <= o["age"] <= 35]

upi_orders = [o for o in orders if o["payment_mode"] == "UPI"]

high_rating = [o for o in orders if o["rating"] and o["rating"] >= 4]

quantity_2 = [o for o in orders if o["quantity"] >= 2]

discount_gt_1000 = [o for o in orders if o["discount"] > 1000]

starts_A = [o for o in orders if o["name"].startswith("A")]

ends_a = [o for o in orders if o["name"].endswith("a")]

contains_h = [o for o in orders if "h" in o["name"].lower()]
```

---

# 🔹 6. Sorting

```python
sorted_total_desc = sorted(orders, key=lambda x: x["total_amount"], reverse=True)

sorted_age = sorted(orders, key=lambda x: x["age"])
```

---

# 🔹 7. Top / Bottom

```python
top5 = sorted(orders, key=lambda x: x["total_amount"], reverse=True)[:5]

bottom3_rating = sorted(orders, key=lambda x: x["rating"] or 0)[:3]
```

---

# 🔹 8. Select with Aliases

```python
result = [
    {
        "Customer_Name": o["name"],
        "Product_Name": o["product"],
        "Total_Sales": o["total_amount"]
    }
    for o in orders
]
```

---

# 🔹 9. Group By Operations

### Group by Category → Total Sales

```python
category_sales = {}

for o in orders:
    category_sales.setdefault(o["category"], 0)
    category_sales[o["category"]] += o["total_amount"]
```

---

### Group by City → Avg Rating

```python
city_ratings = {}

for o in orders:
    city_ratings.setdefault(o["city"], []).append(o["rating"])

city_avg_rating = {
    city: mean(ratings)
    for city, ratings in city_ratings.items()
}
```

---

### Group by Payment Mode → Count

```python
payment_count = {}

for o in orders:
    payment_count[o["payment_mode"]] = payment_count.get(o["payment_mode"], 0) + 1
```

---

### Group by Gender → Avg Age

```python
gender_age = {}

for o in orders:
    gender_age.setdefault(o["gender"], []).append(o["age"])

gender_avg_age = {
    gender: mean(ages)
    for gender, ages in gender_age.items()
}
```

---

# 🔹 10. Aggregations

### Count Distinct Customers

```python
distinct_customers = len(set(o["customer_id"] for o in orders))
```

### Count Distinct Cities

```python
distinct_cities = len(set(o["city"] for o in orders))
```

### Total Revenue

```python
total_revenue = sum(o["total_amount"] for o in orders)
```

### Average Delivery Days

```python
avg_delivery = mean(o["delivery_days"] for o in orders)
```

### Max Delivery Days per City

```python
city_max_delivery = {}

for o in orders:
    city_max_delivery[o["city"]] = max(
        city_max_delivery.get(o["city"], 0),
        o["delivery_days"]
    )
```

---

# 🔹 11. Conditional Columns

```python
for o in orders:
    o["delivery_status"] = "Fast" if o["delivery_days"] <= 3 else "Slow"
    o["high_rating"] = "Yes" if o["rating"] == 5 else "No"
```

---

# 🔹 12. Replace Null Rating with Average

```python
ratings = [o["rating"] for o in orders if o["rating"] is not None]
avg_rating = mean(ratings)

for o in orders:
    if o["rating"] is None:
        o["rating"] = avg_rating
```

---

# 🔹 13. Drop Column

```python
for o in orders:
    o.pop("customer_id", None)
```

---

# 🔹 14. Remove Duplicates (Based on order_id)

```python
unique_orders = {}
for o in orders:
    unique_orders[o["order_id"]] = o

orders = list(unique_orders.values())
```

---

# 🔹 15. String Transformations

### Uppercase Name

```python
for o in orders:
    o["name"] = o["name"].upper()
```

### Lowercase Product

```python
for o in orders:
    o["product"] = o["product"].lower()
```

---

# 🔹 16. Price Category

```python
for o in orders:
    price = o["unit_price"]
    if price < 5000:
        o["price_category"] = "Low"
    elif 5000 <= price <= 30000:
        o["price_category"] = "Medium"
    else:
        o["price_category"] = "High"
```

---

# 🔹 17. Second Highest Total (Window Logic)

```python
totals = sorted(set(o["total_amount"] for o in orders), reverse=True)

second_highest = totals[1] if len(totals) > 1 else None
```

---

# 🚀 How This Maps to PySpark

| PySpark        | Core Python Equivalent  |
| -------------- | ----------------------- |
| withColumn     | Add key in dictionary   |
| filter()       | List comprehension      |
| groupBy        | Dictionary accumulation |
| agg()          | sum(), mean(), max()    |
| orderBy        | sorted()                |
| distinct       | set()                   |
| when/otherwise | if-else                 |
| upper()        | str.upper()             |
| lower()        | str.lower()             |

---
