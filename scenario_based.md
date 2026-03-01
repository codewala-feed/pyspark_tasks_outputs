
# Scenario Based Tasks - Expected outputs

---

# 1️⃣ First Order Status Change Date

```python
src_data = [
    (101, "Placed", "2024-01-01"),
    (101, "Processing", "2024-01-02"),
    (102, "Placed", "2024-02-01"),
    (102, "Processing", "2024-02-03")
]

src_schema = ["order_id", "status", "status_date"]
```

### Expected Output

| order_id | first_status_change_date |
| -------- | ------------------------ |
| 101      | 2024-01-02               |
| 102      | 2024-02-03               |

---

# 2️⃣ Find date when each order moved to 'Shipped' status

```python
src_data = [
    (101, "Placed", "2024-01-01"),
    (101, "Shipped", "2024-01-05"),
    (102, "Placed", "2024-02-01"),
    (102, "Shipped", "2024-02-04")
]

src_schema = ["order_id", "status", "status_date"]
```

### Expected Output

| order_id | shipped_date |
| -------- | ------------ |
| 101      | 2024-01-05   |
| 102      | 2024-02-04   |

---

# 3️⃣ Get most recent status for each order

```python
src_data = [
    (101, "Placed", "2024-01-01"),
    (101, "Delivered", "2024-01-08"),
    (102, "Placed", "2024-02-01"),
    (102, "Cancelled", "2024-02-06")
]

src_schema = ["order_id", "status", "status_date"]
```

### Expected Output

| order_id | latest_status | status_date |
| -------- | ------------- | ----------- |
| 101      | Delivered     | 2024-01-08  |
| 102      | Cancelled     | 2024-02-06  |

---

# 4️⃣ Identify duplicate emails

```python
src_data = [
    ("alice@gmail.com",),
    ("bob@yahoo.com",),
    ("alice@gmail.com",)
]

src_schema = ["email"]
```

### Expected Output

| email                                     | count |
| ----------------------------------------- | ----- |
| [alice@gmail.com](mailto:alice@gmail.com) | 2     |

---

# 5️⃣ Calculate year of birth from age

```python
src_data = [
    ("Alice", 25),
    ("Bob", 30)
]

src_schema = ["name", "age"]
```

### Expected Output (Assume current year 2024)

| name  | age | year_of_birth |
| ----- | --- | ------------- |
| Alice | 25  | 1999          |
| Bob   | 30  | 1994          |

---

# 6️⃣ Calculate running total of sales by customer

```python
src_data = [
    ("A", "2024-01-01", 1000),
    ("A", "2024-01-02", 2000),
    ("B", "2024-01-01", 1500)
]

src_schema = ["customer", "date", "sales"]
```

### Expected Output

| customer | date       | sales | running_total |
| -------- | ---------- | ----- | ------------- |
| A        | 2024-01-01 | 1000  | 1000          |
| A        | 2024-01-02 | 2000  | 3000          |
| B        | 2024-01-01 | 1500  | 1500          |

---

# 7️⃣ Flag customers with more than 1 purchase

```python
src_data = [
    ("A", 101),
    ("A", 102),
    ("B", 103)
]

src_schema = ["customer", "order_id"]
```

### Expected Output

| customer | purchase_count | is_repeat_customer |
| -------- | -------------- | ------------------ |
| A        | 2              | true               |
| B        | 1              | false              |

---

# 8️⃣ Extract domain from email

```python
src_data = [
    ("alice@gmail.com",),
    ("john@yahoo.com",)
]

src_schema = ["email"]
```

### Expected Output

| email                                     | domain    |
| ----------------------------------------- | --------- |
| [alice@gmail.com](mailto:alice@gmail.com) | gmail.com |
| [john@yahoo.com](mailto:john@yahoo.com)   | yahoo.com |

---

# 9️⃣ Mask PAN number

```python
src_data = [
    ("Ravi", "ABCDE1234F"),
    ("Anil", "PQRSX5678K")
]

src_schema = ["name", "pan"]
```

### Expected Output

| name | masked_pan |
| ---- | ---------- |
| Ravi | ABCXXXX34F |
| Anil | PQRSXXX78K |

---

# 🔟 Grade students based on average marks

```python
src_data = [
    ("A", 80, 90),
    ("B", 60, 70)
]

src_schema = ["student", "math", "science"]
```

### Expected Output

| student | avg_marks | grade |
| ------- | --------- | ----- |
| A       | 85        | A     |
| B       | 65        | B     |

---

# 1️⃣1️⃣ Identify customers without orders

```python
src_data = [
    (1, "Alice"),
    (2, "Bob"),
    (3, "Charlie")
]

src_schema = ["customer_id", "name"]
```

(Assume orders exist only for customer_id 1 and 2)

### Expected Output

| customer_id | name    |
| ----------- | ------- |
| 3           | Charlie |

---

# 1️⃣2️⃣ Count products ordered per day

```python
src_data = [
    ("2024-01-01", "P1"),
    ("2024-01-01", "P2"),
    ("2024-01-02", "P3")
]

src_schema = ["order_date", "product"]
```

### Expected Output

| order_date | product_count |
| ---------- | ------------- |
| 2024-01-01 | 2             |
| 2024-01-02 | 1             |

---

# 1️⃣3️⃣ Fill missing dates in time series

```python
src_data = [
    ("2024-01-01", 1000),
    ("2024-01-03", 1500)
]

src_schema = ["date", "sales"]
```

### Expected Output

| date       | sales |
| ---------- | ----- |
| 2024-01-01 | 1000  |
| 2024-01-02 | 0     |
| 2024-01-03 | 1500  |

---

# 1️⃣4️⃣ Pivot category-wise sales per date

```python
src_data = [
    ("2024-01-01", "Electronics", 10000),
    ("2024-01-01", "Clothing", 5000)
]

src_schema = ["date", "category", "sales"]
```

### Expected Output

| date       | Electronics | Clothing |
| ---------- | ----------- | -------- |
| 2024-01-01 | 10000       | 5000     |

---

# 1️⃣5️⃣ Extract initials from full name

```python
src_data = [
    ("Ravi Kumar",),
    ("John Smith",)
]

src_schema = ["full_name"]
```

### Expected Output

| full_name  | initials |
| ---------- | -------- |
| Ravi Kumar | RK       |
| John Smith | JS       |

---

# 1️⃣6️⃣ Sessionize user activity (idle > 30 mins)

```python
src_data = [
    ("U1", "10:00"),
    ("U1", "10:20"),
    ("U1", "11:00")
]

src_schema = ["user", "activity_time"]
```

### Expected Output

| user | session_id |
| ---- | ---------- |
| U1   | 1          |
| U1   | 1          |
| U1   | 2          |

---

# 1️⃣7️⃣ Rank products per user based on total quantity

```python
src_data = [
    ("U1", "A", 5),
    ("U1", "A", 5),
    ("U1", "B", 3)
]

src_schema = ["user", "product", "quantity"]
```

### Expected Output

| user | product | total_qty | rank |
| ---- | ------- | --------- | ---- |
| U1   | A       | 10        | 1    |
| U1   | B       | 3         | 2    |

---

# 1️⃣8️⃣ Calculate rolling 3-day moving average of sales

```python
src_data = [
    ("2024-01-01", 1000),
    ("2024-01-02", 2000),
    ("2024-01-03", 3000)
]

src_schema = ["date", "sales"]
```

### Expected Output

| date       | sales | moving_avg_3d |
| ---------- | ----- | ------------- |
| 2024-01-01 | 1000  | 1000.0        |
| 2024-01-02 | 2000  | 1500.0        |
| 2024-01-03 | 3000  | 2000.0        |

---

# 1️⃣9️⃣ Collapse continuous login periods into date ranges

```python
src_data = [
    ("U1", "2024-01-01"),
    ("U1", "2024-01-02"),
    ("U1", "2024-01-05")
]

src_schema = ["user", "login_date"]
```

### Expected Output

| user | start_date | end_date   |
| ---- | ---------- | ---------- |
| U1   | 2024-01-01 | 2024-01-02 |
| U1   | 2024-01-05 | 2024-01-05 |

---

# 2️⃣0️⃣ Extract top 3 tags from product description

```python
src_data = [
    ("P1", "mobile,5g,android"),
    ("P2", "mobile,android,smart")
]

src_schema = ["product", "tags"]
```

### Expected Output

| product | top_tags               |
| ------- | ---------------------- |
| P1      | [mobile,5g,android]    |
| P2      | [mobile,android,smart] |

---

# 2️⃣1️⃣ Find last non-null value before current row (per user)

```python
src_data = [
    ("U1", "2024-01-01", 100),
    ("U1", "2024-01-02", None),
    ("U1", "2024-01-03", 200)
]

src_schema = ["user", "date", "value"]
```

### Expected Output

| user | date       | value | last_non_null |
| ---- | ---------- | ----- | ------------- |
| U1   | 2024-01-01 | 100   | 100           |
| U1   | 2024-01-02 | null  | 100           |
| U1   | 2024-01-03 | 200   | 200           |

---

# 2️⃣2️⃣ Mask SSN except last 4 digits

```python
src_data = [
    ("Alice", "123456789"),
    ("Bob", "987654321")
]

src_schema = ["name", "ssn"]
```

### Expected Output

| name  | masked_ssn |
| ----- | ---------- |
| Alice | XXXXX6789  |
| Bob   | XXXXX4321  |

---

# 2️⃣3️⃣ Users with more than 2 failed logins in same hour

```python
src_data = [
    ("U1", "10", "failed"),
    ("U1", "10", "failed"),
    ("U1", "10", "failed")
]

src_schema = ["user", "hour", "status"]
```

### Expected Output

| user | hour | failed_count |
| ---- | ---- | ------------ |
| U1   | 10   | 3            |

---

# 2️⃣4️⃣ Flag customers who returned more than bought

```python
src_data = [
    ("C1", 5, 6),
    ("C2", 4, 1)
]

src_schema = ["customer", "bought", "returned"]
```

### Expected Output

| customer | bought | returned | flag  |
| -------- | ------ | -------- | ----- |
| C1       | 5      | 6        | true  |
| C2       | 4      | 1        | false |

---

# 2️⃣5️⃣ Identify price change trend per product

```python
src_data = [
    ("P1", "2024-01-01", 100),
    ("P1", "2024-01-02", 120)
]

src_schema = ["product", "date", "price"]
```

### Expected Output

| product | price_trend |
| ------- | ----------- |
| P1      | Increasing  |

---

# 2️⃣6️⃣ Find pairs of products often bought together

```python id="gq1w8p"
src_data = [
    (1, "A"),
    (1, "B"),
    (2, "A"),
    (2, "B"),
    (3, "A"),
    (3, "C")
]

src_schema = ["order_id", "product"]
```

### Expected Output

| product1 | product2 | frequency |
| -------- | -------- | --------- |
| A        | B        | 2         |

---

# 2️⃣7️⃣ Pivot student grades with best subject

```python id="u7cmz4"
src_data = [
    ("A", "Math", 80),
    ("A", "Science", 90),
    ("B", "Math", 70),
    ("B", "Science", 60)
]

src_schema = ["student", "subject", "marks"]
```

### Expected Output

| student | Math | Science | best_subject |
| ------- | ---- | ------- | ------------ |
| A       | 80   | 90      | Science      |
| B       | 70   | 60      | Math         |

---

# 2️⃣8️⃣ Find common friends from friend pairs

```python id="9u5vbx"
src_data = [
    ("A", "B"),
    ("A", "C"),
    ("B", "C"),
    ("B", "D")
]

src_schema = ["user1", "user2"]
```

### Expected Output

| user1 | user2 | common_friends |
| ----- | ----- | -------------- |
| A     | B     | [C]            |

---

# 2️⃣9️⃣ Identify orders not delivered within 3 days

```python id="x4j3mb"
src_data = [
    (101, "2024-01-01", "2024-01-05"),
    (102, "2024-02-01", "2024-02-02")
]

src_schema = ["order_id", "order_date", "delivery_date"]
```

### Expected Output

| order_id | delayed |
| -------- | ------- |
| 101      | true    |
| 102      | false   |

---

# 3️⃣0️⃣ Calculate total spend and first/last transaction per user

```python id="wpgz8q"
src_data = [
    ("U1", "2024-01-01", 1000),
    ("U1", "2024-01-05", 2000),
    ("U2", "2024-01-03", 1500)
]

src_schema = ["user", "date", "amount"]
```

### Expected Output

| user | total_spend | first_txn  | last_txn   |
| ---- | ----------- | ---------- | ---------- |
| U1   | 3000        | 2024-01-01 | 2024-01-05 |
| U2   | 1500        | 2024-01-03 | 2024-01-03 |

---

# 3️⃣1️⃣ Identify duplicate emails ignoring case

```python id="9tsmz2"
src_data = [
    ("ALICE@gmail.com",),
    ("alice@gmail.com",),
    ("bob@yahoo.com",)
]

src_schema = ["email"]
```

### Expected Output

| email_normalized                          | count |
| ----------------------------------------- | ----- |
| [alice@gmail.com](mailto:alice@gmail.com) | 2     |

---

# 3️⃣2️⃣ Find most viewed product per user

```python id="v6r1tk"
src_data = [
    ("U1", "P1", 5),
    ("U1", "P2", 8),
    ("U2", "P1", 3)
]

src_schema = ["user", "product", "views"]
```

### Expected Output

| user | product | views |
| ---- | ------- | ----- |
| U1   | P2      | 8     |
| U2   | P1      | 3     |

---

# 3️⃣3️⃣ Track running balance for each account

```python id="2klpxf"
src_data = [
    ("A1", "2024-01-01", 1000),
    ("A1", "2024-01-02", -200),
    ("A1", "2024-01-03", 500)
]

src_schema = ["account", "date", "txn_amount"]
```

### Expected Output

| account | date       | running_balance |
| ------- | ---------- | --------------- |
| A1      | 2024-01-01 | 1000            |
| A1      | 2024-01-02 | 800             |
| A1      | 2024-01-03 | 1300            |

---

# 3️⃣4️⃣ Flag last status per order

```python id="1gfdz6"
src_data = [
    (101, "Placed", "2024-01-01"),
    (101, "Delivered", "2024-01-05")
]

src_schema = ["order_id", "status", "status_date"]
```

### Expected Output

| order_id | status    | is_last |
| -------- | --------- | ------- |
| 101      | Placed    | false   |
| 101      | Delivered | true    |

---

# 3️⃣5️⃣ Calculate rolling 3-day sum

```python id="c5q87m"
src_data = [
    ("2024-01-01", 1000),
    ("2024-01-02", 2000),
    ("2024-01-03", 3000)
]

src_schema = ["date", "sales"]
```

### Expected Output

| date       | sales | rolling_sum_3d |
| ---------- | ----- | -------------- |
| 2024-01-01 | 1000  | 1000           |
| 2024-01-02 | 2000  | 3000           |
| 2024-01-03 | 3000  | 6000           |

---

# 3️⃣6️⃣ Calculate employee transfer count

```python id="vmbk71"
src_data = [
    (101, "HR"),
    (101, "Finance"),
    (101, "IT")
]

src_schema = ["emp_id", "department"]
```

### Expected Output

| emp_id | transfer_count |
| ------ | -------------- |
| 101    | 2              |

---

# 3️⃣7️⃣ Rank product sales within category

```python id="e8rk4t"
src_data = [
    ("Electronics", "Mobile", 50000),
    ("Electronics", "Laptop", 30000)
]

src_schema = ["category", "product", "sales"]
```

### Expected Output

| category    | product | sales | rank |
| ----------- | ------- | ----- | ---- |
| Electronics | Mobile  | 50000 | 1    |
| Electronics | Laptop  | 30000 | 2    |

---

# 3️⃣8️⃣ Find ID gaps in sequential table

```python id="7t2nkl"
src_data = [
    (101,),
    (102,),
    (104,)
]

src_schema = ["id"]
```

### Expected Output

| missing_id |
| ---------- |
| 103        |

---

# 3️⃣9️⃣ Identify overlapping date ranges

```python id="2gk0mp"
src_data = [
    (101, "2024-01-01", "2024-01-10"),
    (101, "2024-01-05", "2024-01-15")
]

src_schema = ["emp_id", "start_date", "end_date"]
```

### Expected Output

| emp_id | overlap_flag |
| ------ | ------------ |
| 101    | true         |

---

# 4️⃣0️⃣ Find first purchase channel per customer

```python id="4pqoz7"
src_data = [
    ("C1", "Online", "2024-01-01"),
    ("C1", "Store", "2024-01-05")
]

src_schema = ["customer", "channel", "purchase_date"]
```

### Expected Output

| customer | first_channel |
| -------- | ------------- |
| C1       | Online        |

---

# 4️⃣1️⃣ Count null values per column

```python id="p9v6kl"
src_data = [
    (1, None),
    (2, 10),
    (None, 20)
]

src_schema = ["id", "value"]
```

### Expected Output

| column_name | null_count |
| ----------- | ---------- |
| id          | 1          |
| value       | 1          |

---

# 4️⃣2️⃣ Fill null values in each column with 1

```python id="n3t7yv"
src_data = [
    (1, None),
    (None, 5)
]

src_schema = ["id", "value"]
```

### Expected Output

| id | value |
| -- | ----- |
| 1  | 1     |
| 1  | 5     |

---
