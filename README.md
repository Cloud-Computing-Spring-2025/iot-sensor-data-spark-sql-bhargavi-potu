# 🚀 IoT Sensor Data Analysis using Apache Spark

## 🔍 Overview
This project focuses on processing and analyzing IoT sensor data using Apache Spark. The dataset includes sensor readings such as temperature, humidity, timestamps, and locations. Each task demonstrates a specific analytical operation using Spark SQL and DataFrame transformations.

---

## 📚 Dataset Description
- **sensor_data.csv**: Contains simulated IoT sensor readings.
- Columns:
  - `sensor_id` (Integer)
  - `timestamp` (Timestamp)
  - `temperature` (Float)
  - `humidity` (Float)
  - `location` (String)
  - `sensor_type` (String)

---

## ✅ Tasks & Sample Outputs

### ✨ Task 1: Load & Basic Exploration
**Operations:**
- Load CSV into Spark DataFrame
- Create Temp View
- Show first 5 rows
- Count total records
- Display distinct locations
- Save output to `task1_output.csv`

**Sample Output:**

| sensor_id | timestamp               | temperature | humidity | location          | sensor_type |
|-----------|-------------------------|-------------|----------|-------------------|-------------|
| 1007      | 2025-04-07T11:00:37.000Z| 30.74       | 60.98    | BuildingB_Floor1  | TypeB       |
| 1039      | 2025-04-03T18:50:44.000Z| 18.44       | 51.44    | BuildingA_Floor1  | TypeC       |
| 1004      | 2025-04-05T07:34:26.000Z| 15.58       | 34.04    | BuildingA_Floor1  | TypeC       |
| 1065      | 2025-04-07T15:53:24.000Z| 23.77       | 60.75    | BuildingB_Floor2  | TypeC       |
| 1087      | 2025-04-04T19:02:09.000Z| 31.35       | 35.03    | BuildingB_Floor2  | TypeB       |

---

### 🌡️ Task 2: Filtering & Aggregations
**Operations:**
- Filter out temperatures not in [18, 30]
- Group by location and calculate average temperature & humidity
- Save output to `task2_output.csv`

**Sample Output:**

| location         | avg_temperature       | avg_humidity           |
|------------------|-----------------------|------------------------|
| BuildingB_Floor2 | 25.389874476987462    | 54.19677824267782      |
| BuildingB_Floor1 | 25.168872727272742    | 55.700763636363604     |
| BuildingA_Floor2 | 25.086716417910434    | 54.94197761194029      |
| BuildingA_Floor1 | 24.128669724770635    | 55.12876146788984      |

---

### 🕒 Task 3: Time-Based Analysis
**Operations:**
- Extract hour from timestamp
- Group by hour and find average temperature
- Save output to `task3_output.csv`

**Sample Output:**

| hour_of_day | avg_temp               |
|-------------|------------------------|
| 0           | 23.515277777777783     |
| 1           | 25.736052631578946     |
| 2           | 26.602380952380948     |
| ...         | ...                    |
| 23          | 24.92526315789474      |

---

### 🏋️ Task 4: Ranking Sensors
**Operations:**
- Calculate average temperature per sensor
- Apply window function to rank sensors
- Save output to `task4_output.csv`

**Sample Output:**

| sensor_id | avg_temp              | rank_temp |
|-----------|-----------------------|-----------|
| 1064      | 29.727142857142855    | 1         |
| 1065      | 28.97666666666667     | 2         |
| 1054      | 28.853333333333335    | 3         |
| 1070      | 28.798571428571424    | 4         |
| 1049      | 28.659999999999993    | 5         |

---

### 📊 Task 5: Pivot by Hour
**Operations:**
- Pivot table with location as rows and hour as columns
- Values: average temperature
- Save output to `task5_output.csv`

**Sample Output:**

| location         | 0     | 1     | 2     | ... | 23    |
|------------------|-------|-------|-------|-----|--------|
| BuildingA_Floor1 | 25.23 | 22.21 | 26.28 | ... | 23.58 |
| BuildingB_Floor2 | 24.21 | 27.57 | 26.61 | ... | 25.01 |
| BuildingA_Floor2 | 23.3  | 24.7  | 27.66 | ... | 26.41 |
| BuildingB_Floor1 | 22.07 | 27.34 | 26.02 | ... | 24.67 |

---

## 📊 Analysis & Interpretation
- **Most Active Hours**: Hours 20 and 21 showed the highest average temperatures, suggesting peak sensor activity or hottest times of the day.
- **Hottest Location**: Based on overall averages, `BuildingB_Floor2` recorded the highest average temperatures across all readings.
- **Sensor Rankings**: Sensor `1064` consistently recorded higher temperature readings, ranking first overall.

---

## 🚫 Problems Faced & Fixes
- **Timestamp Format Issues**: Needed to convert string to timestamp using `to_timestamp()` for accurate time-based analysis.
- **Pivot Table Gaps**: Some hours were missing in early tests due to no readings. Ensured full hour range by filtering and restructuring data.
- **Decimal Precision**: Rounded off averages to 2 decimal places for better clarity in final reports.

---

## 📂 Output Files
- `task1_output.csv`
- `task2_output.csv`
- `task3_output.csv`
- `task4_output.csv`
- `task5_output.csv`

---

## 🛠️ Commands to Run Each Task (in Codespaces)
```bash
spark-submit task1.py
spark-submit task2.py
spark-submit task3.py
spark-submit task4.py
spark-submit task5.py
```
---


