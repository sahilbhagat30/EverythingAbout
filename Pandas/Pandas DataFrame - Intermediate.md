# Pandas DataFrame - Intermediate

## Overview
This document explores **intermediate-level operations with Pandas DataFrames**, focusing on data manipulation, grouping, reshaping, and handling missing data. It builds on the basics to provide tools for solving more complex data analysis tasks. Each topic is presented with detailed examples, explanations, and best practices.

---

## Key Topics Covered

### 1. Data Manipulation
#### Adding and Removing Columns
```python
import pandas as pd

# Adding a new column
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35]
}
df = pd.DataFrame(data)
df['City'] = ['New York', 'Los Angeles', 'Chicago']
print(df)

# Removing a column
df = df.drop('City', axis=1)
print(df)
```
**Explanation:**
- **Adding Columns:** Use `df['new_column'] = values` to add a new column. The length of `values` must match the DataFrame rows.
- **Removing Columns:** Use `drop()` with `axis=1` to remove a column.
**Output:**
```
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago

      Name  Age
0    Alice   25
1      Bob   30
2  Charlie   35
```

#### Modifying Data
```python
# Updating column values
df['Age'] = df['Age'] + 1
print(df)
```
**Explanation:**
- Modifying column values is straightforward by performing operations directly on the column.
**Output:**
```
      Name  Age
0    Alice   26
1      Bob   31
2  Charlie   36
```

---

### 2. Grouping and Aggregation
#### Using `groupby`
```python
# Grouping by a column and calculating the mean
data = {
    'Department': ['HR', 'HR', 'IT', 'IT'],
    'Employee': ['Alice', 'Bob', 'Charlie', 'David'],
    'Salary': [60000, 80000, 90000, 85000]
}
df = pd.DataFrame(data)
print(df.groupby('Department')['Salary'].mean())
```
**Explanation:**
- The `groupby()` method groups data by the values in the specified column (`Department`).
- Aggregation functions like `mean()` calculate statistics for each group.
**Output:**
```
Department
HR    70000.0
IT    87500.0
Name: Salary, dtype: float64
```

#### Applying Multiple Aggregations
```python
# Applying multiple aggregation functions
grouped = df.groupby('Department')['Salary'].agg(['mean', 'sum'])
print(grouped)
```
**Explanation:**
- Use `agg()` to apply multiple functions (e.g., `mean`, `sum`) to the grouped data.
- Results are returned in a new DataFrame.
**Output:**
```
                 mean    sum
Department                  
HR          70000.0  140000
IT          87500.0  175000
```

---

### 3. Reshaping and Pivoting
#### Pivot Tables
```python
# Creating a pivot table
data = {
    'Department': ['HR', 'HR', 'IT', 'IT'],
    'Employee': ['Alice', 'Bob', 'Charlie', 'David'],
    'Salary': [70000, 80000, 90000, 85000]
}
df = pd.DataFrame(data)
pivot = df.pivot_table(values='Salary', index='Department', aggfunc='mean')
print(pivot)
```
**Explanation:**
- `pivot_table()` creates a summary table where data is aggregated using functions like `mean()`.
- The `index` parameter specifies the rows, and `values` indicates the column to aggregate.
**Output:**
```
            Salary
Department         
HR          75000.0
IT          87500.0
```

#### Melting
```python
# Melting a DataFrame
data = {
    'Name': ['Alice', 'Bob'],
    'HR': [90, 85],
    'IT': [80, 95]
}
df = pd.DataFrame(data)
melted = pd.melt(df, id_vars='Name', var_name='Department', value_name='Score')
print(melted)
```
**Explanation:**
- The `melt()` function transforms wide-format data into long-format.
- Useful for creating tidy datasets for analysis or visualization.
**Output:**
```
    Name Department  Score
0  Alice         HR     90
1    Bob         HR     85
2  Alice         IT     80
3    Bob         IT     95
```

---

### 4. Handling Missing Data
#### Detecting Missing Data
```python
# Checking for missing values
data = {
    'Name': ['Alice', 'Bob', None],
    'Age': [25, None, 35]
}
df = pd.DataFrame(data)
print(df.isnull())
```
**Explanation:**
- `isnull()` returns a DataFrame of the same shape, with `True` indicating missing values (`NaN`).
**Output:**
```
    Name    Age
0  False  False
1  False   True
2   True  False
```

#### Filling Missing Data
```python
# Filling missing values
df = df.fillna({'Name': 'Unknown', 'Age': df['Age'].mean()})
print(df)
```
**Explanation:**
- Use `fillna()` to replace missing values with specific values or calculated statistics (e.g., mean).
**Output:**
```
      Name   Age
0    Alice  25.0
1      Bob  30.0
2  Unknown  35.0
```

#### Dropping Missing Data
```python
# Dropping rows with missing values
data = {
    'Name': ['Alice', None, 'Charlie'],
    'Age': [25, None, 35]
}
df = pd.DataFrame(data)
df = df.dropna()
print(df)
```
**Explanation:**
- Use `dropna()` to remove rows (default) or columns containing missing values.
**Output:**
```
      Name   Age
0    Alice  25.0
2  Charlie  35.0
```

---

### 5. Intermediate Methods
#### Applying Functions
```python
# Applying a custom function
df['Age'] = df['Age'].apply(lambda x: x + 5)
print(df)
```
**Explanation:**
- The `apply()` function applies a custom operation to each element in a column.
**Output:**
```
      Name   Age
0    Alice  30.0
1      Bob  35.0
2  Unknown  40.0
```

#### Sorting Data
```python
# Sorting by column values
df = df.sort_values(by='Age', ascending=False)
print(df)
```
**Explanation:**
- Use `sort_values()` to sort rows by a specific column in ascending or descending order.
**Output:**
```
      Name   Age
2  Unknown  40.0
1      Bob  35.0
0    Alice  30.0
```

---

### Summary
The **Pandas DataFrame Intermediate** document includes:
- **Data Manipulation**: Adding, removing, and modifying data.
- **Grouping and Aggregation**: Using `groupby` for single and multiple aggregations.
- **Reshaping**: Pivot tables and melting for data reorganization.
- **Handling Missing Data**: Detecting, filling, and dropping missing values.
- **Intermediate Methods**: Applying custom functions and sorting data.

These concepts are essential for solving more complex data analysis tasks and building towards advanced DataFrame operations.

