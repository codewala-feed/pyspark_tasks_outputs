
We’ll assume employee data is stored as a **list of dictionaries** like this:

---

# ✅ Sample Employee Dataset

```python
from statistics import mean, median, stdev
from collections import Counter
import math

employees = [
    {
        "emp_id": 1,
        "first_name": "Akhil",
        "gender": "Male",
        "salary": 60000,
        "city": "Bangalore",
        "job_title": "Data Engineer",
        "latitude": 12.97,
        "longitude": 77.59
    },
    {
        "emp_id": 2,
        "first_name": "Sneha",
        "gender": "Female",
        "salary": 75000,
        "city": "Mumbai",
        "job_title": "Data Scientist",
        "latitude": 19.07,
        "longitude": 72.87
    },
    {
        "emp_id": 3,
        "first_name": "Amit",
        "gender": "Male",
        "salary": 50000,
        "city": "Bangalore",
        "job_title": "Data Analyst",
        "latitude": 12.97,
        "longitude": 77.59
    }
]
```

---

# 🔹 AGGREGATION TASKS

---

## 1️⃣ Average Salary by Gender

```python
gender_salary = {}

for e in employees:
    gender_salary.setdefault(e["gender"], []).append(e["salary"])

avg_salary_gender = {
    g: mean(salaries)
    for g, salaries in gender_salary.items()
}
```

---

## 2️⃣ Median Salary by City

```python
city_salary = {}

for e in employees:
    city_salary.setdefault(e["city"], []).append(e["salary"])

median_salary_city = {
    city: median(salaries)
    for city, salaries in city_salary.items()
}
```

---

## 3️⃣ Max and Min Salary by Gender

```python
max_min_gender = {}

for g, salaries in gender_salary.items():
    max_min_gender[g] = {
        "max": max(salaries),
        "min": min(salaries)
    }
```

---

## 4️⃣ Count Employees per Job Title

```python
job_count = {}

for e in employees:
    job_count[e["job_title"]] = job_count.get(e["job_title"], 0) + 1
```

---

## 5️⃣ Most Common First Name

```python
name_counts = Counter(e["first_name"] for e in employees)
most_common_name = name_counts.most_common(1)
```

---

## 6️⃣ Gender Distribution per Job Title

```python
job_gender = {}

for e in employees:
    job_gender.setdefault(e["job_title"], []).append(e["gender"])

gender_distribution = {
    job: dict(Counter(genders))
    for job, genders in job_gender.items()
}
```

---

## 7️⃣ Total Salary per Gender

```python
total_salary_gender = {
    g: sum(salaries)
    for g, salaries in gender_salary.items()
}
```

---

## 8️⃣ Max & Min Salary per City

```python
city_max_min = {}

for city, salaries in city_salary.items():
    city_max_min[city] = {
        "max": max(salaries),
        "min": min(salaries)
    }
```

---

## 9️⃣ Top 5 Cities by Average Salary

```python
city_avg_salary = {
    city: mean(salaries)
    for city, salaries in city_salary.items()
}

top5_cities = sorted(
    city_avg_salary.items(),
    key=lambda x: x[1],
    reverse=True
)[:5]
```

---

## 🔟 Avg Salary by (City, Job Title)

```python
city_job_salary = {}

for e in employees:
    key = (e["city"], e["job_title"])
    city_job_salary.setdefault(key, []).append(e["salary"])

avg_city_job = {
    key: mean(salaries)
    for key, salaries in city_job_salary.items()
}
```

---

## 1️⃣1️⃣ Employees Above Overall Average

```python
overall_avg = mean(e["salary"] for e in employees)

above_avg_count = len(
    [e for e in employees if e["salary"] > overall_avg]
)
```

---

## 1️⃣2️⃣ Unique Job Titles

```python
unique_jobs = len(set(e["job_title"] for e in employees))
```

---

## 1️⃣3️⃣ Gender % per City

```python
city_gender = {}

for e in employees:
    city_gender.setdefault(e["city"], []).append(e["gender"])

percentage_gender_city = {}

for city, genders in city_gender.items():
    total = len(genders)
    counts = Counter(genders)
    percentage_gender_city[city] = {
        g: (c / total) * 100
        for g, c in counts.items()
    }
```

---

## 1️⃣4️⃣ Avg Latitude & Longitude per City

```python
city_geo = {}

for e in employees:
    city_geo.setdefault(e["city"], []).append((e["latitude"], e["longitude"]))

avg_geo_city = {}

for city, coords in city_geo.items():
    avg_lat = mean(lat for lat, _ in coords)
    avg_lon = mean(lon for _, lon in coords)
    avg_geo_city[city] = (avg_lat, avg_lon)
```

---

## 1️⃣5️⃣ Top 3 Job Titles by Avg Salary

```python
job_salary = {}

for e in employees:
    job_salary.setdefault(e["job_title"], []).append(e["salary"])

job_avg = {
    job: mean(salaries)
    for job, salaries in job_salary.items()
}

top3_jobs = sorted(
    job_avg.items(),
    key=lambda x: x[1],
    reverse=True
)[:3]
```

---

## 1️⃣6️⃣ Std Deviation of Salary per Job

```python
job_std_dev = {
    job: stdev(salaries) if len(salaries) > 1 else 0
    for job, salaries in job_salary.items()
}
```

---

## 1️⃣7️⃣ Correlation Between Latitude & Longitude

```python
latitudes = [e["latitude"] for e in employees]
longitudes = [e["longitude"] for e in employees]

mean_lat = mean(latitudes)
mean_lon = mean(longitudes)

numerator = sum(
    (lat - mean_lat) * (lon - mean_lon)
    for lat, lon in zip(latitudes, longitudes)
)

denominator = math.sqrt(
    sum((lat - mean_lat) ** 2 for lat in latitudes) *
    sum((lon - mean_lon) ** 2 for lon in longitudes)
)

correlation = numerator / denominator if denominator != 0 else 0
```

---

# 🔹 DATA FILTERING TASKS

---

## Salary Above Threshold

```python
high_salary = [e for e in employees if e["salary"] > 70000]
```

---

## Specific City

```python
bangalore_emp = [e for e in employees if e["city"] == "Bangalore"]
```

---

## By Gender

```python
female_emp = [e for e in employees if e["gender"] == "Female"]
```

---

## Job Title Contains Keyword

```python
data_jobs = [
    e for e in employees
    if "Data" in e["job_title"]
]
```

---

## Salary Within Range

```python
range_salary = [
    e for e in employees
    if 50000 <= e["salary"] <= 80000
]
```

---

## Filter by List of Cities

```python
cities = ["Bangalore", "Mumbai"]

filtered_cities = [
    e for e in employees
    if e["city"] in cities
]
```

---

## Missing / Null Values

```python
missing_values = [
    e for e in employees
    if any(value is None for value in e.values())
]
```

---

## Specific Job Title

```python
engineers = [
    e for e in employees
    if e["job_title"] == "Data Engineer"
]
```

---

## First Name Starts With Letter

```python
starts_A = [
    e for e in employees
    if e["first_name"].startswith("A")
]
```

---

## Multiple Conditions (City + Gender)

```python
filtered_combo = [
    e for e in employees
    if e["city"] == "Bangalore" and e["gender"] == "Male"
]
```

---

# 🚀 What You Just Practiced

| PySpark Concept | Core Python Equivalent  |
| --------------- | ----------------------- |
| groupBy         | dictionary + setdefault |
| agg             | sum, mean, median, max  |
| filter          | list comprehension      |
| withColumn      | add new key             |
| distinct        | set()                   |
| orderBy         | sorted()                |
| window logic    | sorted + slicing        |
| correlation     | manual formula          |

---
