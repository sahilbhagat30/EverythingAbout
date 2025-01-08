# Pandas DataFrame - Advanced

## Overview
This document explores **advanced-level operations with Pandas DataFrames**, focusing on performance optimization, multi-indexing, time-series analysis, and exporting data. It provides tools for handling complex data tasks with efficiency and clarity.

---

## Key Topics Covered

### 1. MultiIndex DataFrames
#### Creating a MultiIndex
```python
import pandas as pd

# MultiIndex example
data = [
    ['Alice', 'HR', 70000],
    ['Bob', 'HR', 80000],
    ['Charlie', 'IT', 90000]
]
index = pd.MultiIndex.from_tuples(
    [('HR', 'Alice'), ('HR', 'Bob'), ('IT', 'Charlie')],
    names=['Department', 'Employee']
)
df = pd.DataFrame(data, index=index, columns=['Name', 'Position', 'Salary'])
print(df)
```
**Explanation:**
- MultiIndex organizes data into hierarchical levels, making it easier to represent and manipulate.
**Output:**
```
                        Name  Position  Salary
Department Employee                          
HR         Alice       Alice        HR   70000
           Bob         Bob          HR   80000
IT         Charlie     Charlie      IT   90000
```

#### Accessing Data in a MultiIndex
```python
# Accessing data at specific levels
print(df.loc['HR'])

# Accessing data for a specific employee
print(df.loc[('HR', 'Alice')])
```
**Output:**
```
           Name Position  Salary
Employee                       
Alice      Alice      HR   70000
Bob          Bob      HR   80000
Name       Alice
Position      HR
Salary     70000
```

---

### 2. Performance Optimization
#### Using `eval` and `query`
```python
# Using eval and query for efficient operations
data = {
    'A': [1, 2, 3],
    'B': [4, 5, 6],
    'C': [7, 8, 9]
}
df = pd.DataFrame(data)
df['Sum'] = df.eval("A + B + C")
filtered = df.query("A > 1 and B < 6")
print(df)
print(filtered)
```
**Explanation:**
- `eval`: Adds new columns with calculated values efficiently.
- `query`: Filters rows based on complex conditions using strings.
**Output:**
```
   A  B  C  Sum
0  1  4  7   12
1  2  5  8   15
2  3  6  9   18
   A  B  C  Sum
1  2  5  8   15
```

#### Memory Optimization
```python
# Converting columns to categorical types
data = {
    'Category': ['A', 'B', 'A', 'C'],
    'Values': [10, 20, 15, 25]
}
df = pd.DataFrame(data)
df['Category'] = df['Category'].astype('category')
print(df.info())
```
**Explanation:**
- Reduces memory usage by converting text data to `category` type.
**Output:**
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 4 entries, 0 to 3
Data columns (total 2 columns):
 #   Column    Non-Null Count  Dtype   
---  ------    --------------  -----   
 0   Category  4 non-null      category
 1   Values    4 non-null      int64   
dtypes: category(1), int64(1)
memory usage: 436.0 bytes
```

---

### 3. Time-Series Analysis
#### Working with Datetime Index
```python
# Creating a DataFrame with datetime index
data = {
    'Sales': [250, 300, 400]
}
dates = pd.date_range(start='2023-01-01', periods=3, freq='D')
df = pd.DataFrame(data, index=dates)
print(df)
```
**Explanation:**
- `date_range` creates a range of dates to serve as the index.
**Output:**
```
            Sales
2023-01-01    250
2023-01-02    300
2023-01-03    400
```

#### Resampling Time-Series Data
```python
# Resampling to calculate weekly totals
weekly = df.resample('W').sum()
print(weekly)
```
**Explanation:**
- Resampling aggregates data over specified time intervals.
**Output:**
```
            Sales
2023-01-08    950
```

---

### 4. Advanced Missing Data Handling
#### Interpolation
```python
# Interpolating missing values
data = {
    'Time': [1, 2, 3, 4, 5],
    'Value': [10, None, None, 40, 50]
}
df = pd.DataFrame(data)
df['Value'] = df['Value'].interpolate()
print(df)
```
**Explanation:**
- `interpolate()` fills missing values using linear interpolation.
**Output:**
```
   Time  Value
0     1   10.0
1     2   20.0
2     3   30.0
3     4   40.0
4     5   50.0
```

---

### 5. Exporting Data
#### Exporting to CSV
```python
# Exporting to a CSV file
data = {
    'Name': ['Alice', 'Bob'],
    'Age': [25, 30]
}
df = pd.DataFrame(data)
df.to_csv('output.csv', index=False)
print("Data exported to 'output.csv'")
```

#### Exporting to Excel
```python
# Exporting to an Excel file
# Uncomment to execute
# df.to_excel('output.xlsx', index=False)
# print("Data exported to 'output.xlsx'")
```

---

### Summary
The **Pandas DataFrame Advanced** document includes:
- **MultiIndex DataFrames**: Hierarchical indexing and data access.
- **Performance Optimization**: Efficient computations and memory management.
- **Time-Series Analysis**: Working with datetime data and resampling.
- **Advanced Missing Data Handling**: Using interpolation for filling gaps.
- **Exporting Data**: Saving DataFrames to files (CSV, Excel).

These topics provide tools for handling complex data analysis tasks with efficiency and precision.

