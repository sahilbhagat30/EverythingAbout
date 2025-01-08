# Pandas DataFrame - Basics

## Overview
This document introduces the **basics of Pandas DataFrame**, covering essential topics for beginners to understand the core functionalities of DataFrames. It focuses on creating, indexing, slicing, and exploring fundamental operations for effective data analysis.

---

## Key Topics Covered

### 1. Introduction
A Pandas DataFrame is a two-dimensional labeled data structure that organizes data in rows and columns, similar to a spreadsheet or SQL table. It is highly versatile and can hold heterogeneous data types (integers, strings, floats, etc.).

---

### 2. Creation
#### Creating a DataFrame from a Dictionary
```python
import pandas as pd

# Creating a DataFrame from a dictionary
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'Los Angeles', 'Chicago']
}
df = pd.DataFrame(data)
print(df)
```
**Output:**
```
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

#### Creating a DataFrame from a List of Lists
```python
# Creating a DataFrame from a list of lists
data = [
    ['Alice', 25, 'New York'],
    ['Bob', 30, 'Los Angeles'],
    ['Charlie', 35, 'Chicago']
]
df = pd.DataFrame(data, columns=['Name', 'Age', 'City'])
print(df)
```
**Output:**
```
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

#### Creating a DataFrame from a CSV File
```python
# Reading from a CSV file
# Uncomment the line below to execute
# df = pd.read_csv('data.csv')
# print(df)
```
**Output:**
- Reads tabular data from a CSV file into a DataFrame.
- Automatically infers column names from the first row of the file.

---

### 3. Indexing and Slicing
#### Using `.loc` for Label-Based Indexing
```python
# Selecting rows and columns by labels
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'Los Angeles', 'Chicago']
}
df = pd.DataFrame(data)

# Accessing a single value by label
print(df.loc[0, 'Name'])  # Output: Alice

# Selecting multiple rows and specific columns
print(df.loc[0:1, ['Name', 'City']])
```
**Output:**
```
      Name         City
0    Alice     New York
1      Bob  Los Angeles
```

#### Using `.iloc` for Positional Indexing
```python
# Selecting rows and columns by position
print(df.iloc[1, 0])  # Output: Bob

# Selecting all rows for specific columns
print(df.iloc[:, [0, 2]])
```
**Output:**
```
      Name         City
0    Alice     New York
1      Bob  Los Angeles
2  Charlie      Chicago
```

#### Boolean Indexing
```python
# Filtering rows based on a condition
print(df[df['Age'] > 25])
```
**Output:**
```
      Name  Age         City
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

---

### 4. Attributes
#### Common Attributes of a DataFrame
```python
# Example of DataFrame attributes
print("Shape:", df.shape)         # Tuple of (rows, columns)
print("Columns:", df.columns)   # List of column labels
print("Index:", df.index)       # Index labels for rows
print("Data Types:", df.dtypes) # Data types of each column
```
**Output:**
```
Shape: (3, 3)
Columns: Index(['Name', 'Age', 'City'], dtype='object')
Index: RangeIndex(start=0, stop=3, step=1)
Data Types: Name    object
Age      int64
City    object
dtype: object
```

---

### 5. Basic Methods
#### Viewing Data
```python
# Viewing the first few rows
df.head()

# Viewing the last few rows
df.tail()
```
**Output:**
- `.head()`: Displays the first 5 rows by default.
- `.tail()`: Displays the last 5 rows by default.

#### Descriptive Statistics
```python
# Generating summary statistics
print(df.describe())
```
**Output:**
- Provides statistics like mean, count, min, and max for numeric columns.

---

### Summary
This document covers:
- DataFrame creation from various sources (dictionaries, lists, CSVs).
- Indexing and slicing using `.loc`, `.iloc`, and Boolean indexing.
- Attributes to explore structure and data types.
- Basic methods for inspecting and summarizing data.

The **Pandas DataFrame Basics** document provides the foundation needed to manipulate and analyze tabular data effectively. For more advanced operations, refer to the intermediate and advanced documents.

