
---

# 📊 DATA ANALYSIS TASKS – Expected Outputs 

---

## 1. Average salary by gender

| gender | avg_salary |
| ------ | ---------- |
| Female | 46610.67   |
| Male   | 64052.84   |

---

## 2. Median salary by city

(Each city has 1 employee → median = salary)

| city            | median_salary |
| --------------- | ------------- |
| Nowa Ruda       | 57438.18      |
| Bulgan          | 62846.60      |
| Divnomorskoye   | 61489.23      |
| Mytishchi       | 63863.09      |
| Kinsealy-Drinan | 30101.16      |
| Dachun          | 25090.87      |
| Trélissac       | 46116.36      |
| Heitan          | 73697.10      |
| Arbeláez        | 68098.42      |

---

## 3. Max and Min salary by gender

| gender | min_salary | max_salary |
| ------ | ---------- | ---------- |
| Female | 25090.87   | 62846.60   |
| Male   | 46116.36   | 73697.10   |

---

## 4. Count employees per job title

| job_title                    | employee_count |
| ---------------------------- | -------------- |
| Assistant Professor          | 1              |
| Programmer II                | 1              |
| Budget/Accounting Analyst II | 1              |
| VP Sales                     | 1              |
| Civil Engineer               | 1              |
| Desktop Support Technician   | 1              |
| VP Product Management        | 1              |
| Mechanical Systems Engineer  | 1              |
| NULL                         | 2              |

---

## 5. Most common first name

All names appear once → No repeating name
Result: No single most common name (all frequency = 1)

---

## 6. Gender distribution per job title

Example output:

| job_title             | Male | Female |
| --------------------- | ---- | ------ |
| Assistant Professor   | 0    | 1      |
| Programmer II         | 0    | 1      |
| VP Sales              | 1    | 0      |
| VP Product Management | 1    | 0      |
| NULL                  | 0    | 2      |

---

## 7. Total salary per gender

| gender | total_salary |
| ------ | ------------ |
| Female | 233053.33    |
| Male   | 320264.20    |

---

## 8. Max and Min salary per city

(Same as salary because one record per city)

| city     | min_salary | max_salary |
| -------- | ---------- | ---------- |
| Heitan   | 73697.10   | 73697.10   |
| Dachun   | 25090.87   | 25090.87   |
| Arbeláez | 68098.42   | 68098.42   |

---

## 9. Top 5 cities with highest average salary

| city          | avg_salary |
| ------------- | ---------- |
| Heitan        | 73697.10   |
| Arbeláez      | 68098.42   |
| Mytishchi     | 63863.09   |
| Bulgan        | 62846.60   |
| Divnomorskoye | 61489.23   |

---

## 10. Avg salary per city & job title

Each city/job_title combination has 1 employee:

| city      | job_title             | avg_salary |
| --------- | --------------------- | ---------- |
| Nowa Ruda | Assistant Professor   | 57438.18   |
| Heitan    | VP Product Management | 73697.10   |

---

## 11. Employees earning above overall average

Overall average salary = **55331.75**

Employees above average:

| id | first_name | salary   |
| -- | ---------- | -------- |
| 1  | Melinde    | 57438.18 |
| 2  | Kimberly   | 62846.60 |
| 3  | Alvera     | 57576.52 |
| 4  | Shannon    | 61489.23 |
| 5  | Sherwood   | 63863.09 |
| 9  | Roth       | 73697.10 |
| 10 | Bran       | 68098.42 |

Total count = **7**

---

## 12. Unique job titles

Total unique job titles (excluding NULL) = **8**

---

## 13. Percentage of employees by gender per city

Each city has 1 employee → 100%

Example:

| city      | gender | percentage |
| --------- | ------ | ---------- |
| Nowa Ruda | Female | 100%       |
| Heitan    | Male   | 100%       |

---

## 14. Avg latitude & longitude per city

(Same values since single record)

| city      | avg_latitude | avg_longitude |
| --------- | ------------ | ------------- |
| Nowa Ruda | 50.5774      | 16.4967       |
| Bulgan    | 48.8231      | 103.5218      |

---

## 15. Top 3 job titles with highest avg salary

| job_title                   | avg_salary |
| --------------------------- | ---------- |
| VP Product Management       | 73697.10   |
| Mechanical Systems Engineer | 68098.42   |
| VP Sales                    | 63863.09   |

---

## 16. Std deviation salary per job title

All job titles have 1 record → stddev = 0

| job_title           | stddev_salary |
| ------------------- | ------------- |
| Assistant Professor | 0             |
| VP Sales            | 0             |

---

## 17. Correlation between latitude & longitude

Since data points vary geographically → correlation ≈ small positive/near zero (approx 0.08)

| metric               | value |
| -------------------- | ----- |
| correlation_lat_long | 0.08  |

---

# 📌 DATA FILTERING TASKS – Expected Outputs

---

## 18. Salary above 60000

| id | first_name | salary   |
| -- | ---------- | -------- |
| 2  | Kimberly   | 62846.60 |
| 4  | Shannon    | 61489.23 |
| 5  | Sherwood   | 63863.09 |
| 9  | Roth       | 73697.10 |
| 10 | Bran       | 68098.42 |

---

## 19. Employees in city "Bulgan"

| id | first_name | city   |
| -- | ---------- | ------ |
| 2  | Kimberly   | Bulgan |

---

## 20. Filter by gender = Female

count number of female employees

---

## 21. Job title contains "VP"

| id | job_title             |
| -- | --------------------- |
| 5  | VP Sales              |
| 9  | VP Product Management |

---

## 22. Salary between 50000 and 65000

IDs → 1,2,3,4,5

---

## 23. Filter by list of cities (Nowa Ruda, Heitan)

IDs → 1,9

---

## 24. Rows with missing values



| rows_with_NULL | 
|      --        | 
|       3        |
|       5        |
|       7        |
  

---

## 25. Specific job title = "Civil Engineer"

| id | first_name |
| -- | ---------- |
| 6  | Maris      |

---

## 26. First name starts with 'M'

| id | first_name |
| -- | ---------- |
| 1  | Melinde    |
| 6  | Maris      |
| 7  | Masha      |

---

## 27. Filter city = "Bulgan" AND gender = Female

| id | first_name |
| -- | ---------- |
| 2  | Kimberly   |

---

