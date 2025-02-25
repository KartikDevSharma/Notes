# **Pandas: Beginner-Friendly Guide**  

Pandas is a **Python library** for **data manipulation and analysis**. It provides **data structures** like **Series** and **DataFrame** that allow us to work with structured data efficiently.  

---

## **1. Importing Pandas**
```python
import pandas as pd  # Standard convention
```

---

## **2. Pandas Data Structures**  

### **a) Series (1D Data)**
A **Series** is like a **column** in a spreadsheet. It is a **one-dimensional labeled array**.

```python
data = [10, 20, 30, 40]
series = pd.Series(data)
print(series)
```
**Output:**  
```
0    10
1    20
2    30
3    40
dtype: int64
```
🔹 The left column (0,1,2,3) is the **index**, and the right column contains the **values**.

#### **Custom Index**
```python
series = pd.Series([10, 20, 30], index=['a', 'b', 'c'])
print(series)
```
**Output:**
```
a    10
b    20
c    30
dtype: int64
```

#### **Accessing Elements**
```python
print(series['a'])  # Output: 10
```

---

### **b) DataFrame (2D Data)**
A **DataFrame** is like a **table** with **rows and columns**.

```python
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
}

df = pd.DataFrame(data)
print(df)
```
**Output:**
```
     Name  Age  Salary
0   Alice   25  50000
1     Bob   30  60000
2  Charlie   35  70000
```

#### **Accessing Columns**
```python
print(df['Name'])  # Output: Only the "Name" column
```

#### **Accessing Rows**
```python
print(df.iloc[1])  # Get the second row (index 1)
print(df.loc[0])   # Get the first row by label
```

---

## **3. Reading and Writing Data**
### **Reading CSV Files**
```python
df = pd.read_csv("data.csv")  # Load data from a CSV file
print(df.head())  # Show first 5 rows
```

### **Writing to CSV**
```python
df.to_csv("output.csv", index=False)  # Save without index column
```

---

## **4. Basic Operations**
### **Checking Data**
```python
print(df.info())    # Summary of the DataFrame
print(df.describe())  # Statistical summary
print(df.shape)  # (rows, columns)
print(df.columns)  # List of column names
print(df.dtypes)  # Data types of each column
```

### **Filtering Data**
```python
df_filtered = df[df['Age'] > 28]  # Get only rows where Age > 28
print(df_filtered)
```

### **Sorting Data**
```python
df_sorted = df.sort_values(by='Salary', ascending=False)  # Sort by Salary (descending)
```

---

## **5. Modifying Data**
### **Adding a Column**
```python
df['Bonus'] = df['Salary'] * 0.10  # Create a new column
```

### **Updating Values**
```python
df.loc[df['Name'] == 'Alice', 'Salary'] = 55000  # Change Alice's salary
```

### **Removing a Column**
```python
df = df.drop(columns=['Bonus'])  # Remove 'Bonus' column
```

### **Removing a Row**
```python
df = df.drop(index=1)  # Remove row at index 1
```

---

## **6. Handling Missing Data**
### **Checking for Missing Values**
```python
print(df.isnull().sum())  # Count missing values in each column
```

### **Filling Missing Values**
```python
df.fillna(0, inplace=True)  # Replace NaN with 0
```

### **Dropping Rows with Missing Values**
```python
df.dropna(inplace=True)
```

---

## **7. Grouping and Aggregation**
### **Grouping Data**
```python
df_grouped = df.groupby('Age').mean()  # Group by 'Age' and compute mean
print(df_grouped)
```

### **Aggregating Multiple Columns**
```python
df.agg({'Salary': 'mean', 'Age': 'max'})  # Compute mean salary and max age
```

---

## **8. Merging and Joining Data**
### **Concatenation**
```python
df1 = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
df2 = pd.DataFrame({'A': [5, 6], 'B': [7, 8]})
df_combined = pd.concat([df1, df2])  # Stack DataFrames
```

### **Merging DataFrames (Like SQL JOIN)**
```python
df1 = pd.DataFrame({'ID': [1, 2, 3], 'Name': ['Alice', 'Bob', 'Charlie']})
df2 = pd.DataFrame({'ID': [1, 2, 4], 'Salary': [50000, 60000, 70000]})

df_merged = pd.merge(df1, df2, on='ID', how='inner')  # Inner Join
```

---

## **9. Pivot Tables**
```python
df.pivot_table(index='Name', values='Salary', aggfunc='mean')
```

---

## **10. Time Series Analysis**
```python
df['Date'] = pd.to_datetime(df['Date'])  # Convert to datetime
df.set_index('Date', inplace=True)  # Set Date column as index
print(df.resample('M').mean())  # Monthly average
```

---

## **Interview Summary (Important Points)**
1️⃣ **Pandas provides Series (1D) and DataFrame (2D) for handling structured data.**  
2️⃣ **You can read/write data using `read_csv()` and `to_csv()`.**  
3️⃣ **Filtering, sorting, and modifying data is easy with Pandas.**  
4️⃣ **Missing data can be handled using `fillna()` and `dropna()`.**  
5️⃣ **Pandas supports powerful data aggregation (`groupby()`, `pivot_table()`).**  
6️⃣ **Joining and merging data is possible using `merge()` and `concat()`.**  
7️⃣ **Time series data can be processed using `resample()` and `to_datetime()`.**  

---

# **Understanding Pandas DataFrame in a Beginner-Friendly Way**  

A **DataFrame** in Pandas is like an **Excel spreadsheet or a table in SQL**. It is a **2D structure** that consists of **rows and columns**, making it perfect for handling structured data like CSV files, databases, and API responses.

## **1. What is a DataFrame?**
A **DataFrame** is essentially:  
✅ A **table** with labeled rows and columns  
✅ Each **column** can have a different **data type** (numbers, strings, dates, etc.)  
✅ Supports **indexing, filtering, sorting, and transformations** easily  

### **Creating a DataFrame**
```python
import pandas as pd

data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'Salary': [50000, 60000, 70000]
}

df = pd.DataFrame(data)
print(df)
```
**Output:**
```
     Name  Age  Salary
0   Alice   25  50000
1     Bob   30  60000
2  Charlie   35  70000
```
- The **column names** are `"Name"`, `"Age"`, and `"Salary"`.  
- The **index** (left-most numbers) is automatically created (`0, 1, 2`).  
- Each column has a **different data type** (`str`, `int`, `int`).  

---

## **2. Why Does `axis` Matter?**  
Whenever we perform operations on rows or columns, **Pandas needs to know** whether we are modifying:  
- **Rows (axis=0)** → Vertical direction (downwards)  
- **Columns (axis=1)** → Horizontal direction (sideways)  

Let's see how this works with **dropping rows and columns**.

### **a) Dropping Rows (`axis=0`)**
Rows are identified using the **index** (0, 1, 2...).

```python
df_dropped_rows = df.drop(1, axis=0)  # Drop row at index 1 (Bob)
print(df_dropped_rows)
```
**Output:**
```
     Name  Age  Salary
0   Alice   25  50000
2  Charlie   35  70000
```
- **Row at index `1` (Bob) was removed** because we set `axis=0` (rows).  
- The rest of the table remains **unchanged**.  

### **b) Dropping Columns (`axis=1`)**
Columns are identified using the **column name**.

```python
df_dropped_cols = df.drop('Salary', axis=1)  # Drop the "Salary" column
print(df_dropped_cols)
```
**Output:**
```
     Name  Age
0   Alice   25
1     Bob   30
2  Charlie   35
```
- The **Salary column** was removed because we set `axis=1` (columns).  
- All rows remain the same.  

🔹 **Key Rule to Remember**:  
- **axis=0 → Works on rows**  
- **axis=1 → Works on columns**  

---

## **3. What is `inplace=True`?**  
Normally, **Pandas does not modify the original DataFrame**.  
Instead, it **returns a new modified DataFrame** and leaves the original unchanged.  

```python
df.drop('Salary', axis=1)  # Does NOT modify df directly!
print(df)  # "Salary" column still exists!
```

🔹 If we want to **modify the original DataFrame**, we use `inplace=True`.

```python
df.drop('Salary', axis=1, inplace=True)  # Modify df directly
print(df)
```
Now, `"Salary"` is **permanently removed from `df`**.

### **When to Use `inplace=True`?**
✅ Use `inplace=True` when you want to **modify the original DataFrame**  
❌ Avoid `inplace=True` if you want to keep the original data and create a **new version**  

---

## **4. Selecting Data from a DataFrame**
### **a) Selecting a Single Column**
```python
print(df['Name'])  # Get the "Name" column
```
**Output:**
```
0    Alice
1      Bob
2  Charlie
Name: Name, dtype: object
```
- This returns a **Series** (1D), not a full DataFrame.

### **b) Selecting Multiple Columns**
```python
print(df[['Name', 'Age']])  # Get "Name" and "Age"
```
**Output:**
```
     Name  Age
0   Alice   25
1     Bob   30
2  Charlie   35
```
🔹 Always use **double brackets** `[['column1', 'column2']]` for multiple columns.

---

## **5. Selecting Rows (`iloc` and `loc`)**
Pandas allows **row selection** using two main methods:

### **a) Selecting by Position (`iloc`)**
Use **index numbers** (like lists).

```python
print(df.iloc[1])  # Get the second row (index 1)
```
**Output:**
```
Name      Bob
Age        30
Salary  60000
Name: 1, dtype: object
```

### **b) Selecting by Label (`loc`)**
Use **index labels** (useful if indexes are names).

```python
print(df.loc[0])  # Get the first row (index 0)
```
**Same output as above.**

---

## **6. Filtering Data**
We can **filter rows** based on conditions.

```python
df_filtered = df[df['Age'] > 28]  # Only people older than 28
print(df_filtered)
```
**Output:**
```
     Name  Age  Salary
1     Bob   30  60000
2  Charlie   35  70000
```
- Only Bob and Charlie remain because their Age > 28.

---

## **7. Adding and Removing Columns**
### **Adding a New Column**
```python
df['Bonus'] = df['Salary'] * 0.10  # 10% bonus for everyone
```

### **Renaming Columns**
```python
df.rename(columns={'Salary': 'Annual Salary'}, inplace=True)
```

---

## **8. Handling Missing Values**
### **Checking for Missing Data**
```python
print(df.isnull().sum())  # Count missing values
```

### **Filling Missing Values**
```python
df.fillna(0, inplace=True)  # Replace NaN with 0
```

### **Dropping Rows with Missing Values**
```python
df.dropna(inplace=True)  # Remove rows with missing data
```

---

## **9. Sorting Data**
### **Sorting by a Column**
```python
df_sorted = df.sort_values(by='Salary', ascending=False)  # Highest Salary first
```

---

## **10. Grouping and Aggregation**
```python
df.groupby('Age').mean()  # Average values grouped by Age
```

---

## **Interview Summary (Key Takeaways)**
✅ **DataFrame is like an Excel table with rows and columns.**  
✅ **Use `axis=0` for rows, `axis=1` for columns (e.g., `drop()`).**  
✅ **`inplace=True` modifies the original DataFrame, otherwise, a new one is returned.**  
✅ **Select data using `iloc[]` (position) and `loc[]` (label).**  
✅ **Filtering is easy with conditions like `df[df['Age'] > 30]`.**  
✅ **Handle missing data using `fillna()` or `dropna()`.**  
✅ **Use `groupby()` for aggregations like sum, mean, etc.**  



---

# **Working with CSV Files in Pandas (Beginner-Friendly Guide)**  

CSV (Comma-Separated Values) files are **one of the most common formats** for storing tabular data.  
Pandas makes it **super easy** to read, write, and manipulate CSV files.  

---

## **1. Reading a CSV File**  
The first step in working with CSV files is to load them into a **Pandas DataFrame**.

### **🔹 Basic CSV File Reading**
```python
import pandas as pd

df = pd.read_csv("data.csv")  # Load CSV into a DataFrame
print(df.head())  # Show first 5 rows
```
✅ **`pd.read_csv()`** automatically detects **columns and rows** from the CSV file.  
✅ **`head()`** helps in previewing the first 5 rows.  

---

## **2. Understanding the Data**  
After loading the data, you should always **check its structure**.

### **🔹 Getting General Information**
```python
print(df.info())  # Summary of the DataFrame
print(df.shape)   # (Rows, Columns)
print(df.columns) # List of column names
```
✅ **`info()`** shows **data types**, **missing values**, and **memory usage**.  
✅ **`shape`** tells how many **rows and columns** exist.  

### **🔹 Checking for Missing Values**
```python
print(df.isnull().sum())  # Count missing values in each column
```

---

## **3. Selecting Specific Columns and Rows**
### **🔹 Selecting Specific Columns**
```python
print(df['Name'])  # Get a single column
print(df[['Name', 'Salary']])  # Get multiple columns
```

### **🔹 Selecting Specific Rows**
```python
print(df.loc[0])   # Select row with index 0
print(df.iloc[2])  # Select the third row (position-based)
```

---

## **4. Writing Data to a CSV File**
Once we modify the data, we often need to **save it back** to a CSV file.

### **🔹 Saving Data to CSV**
```python
df.to_csv("new_data.csv", index=False)  # Save without the index column
```
✅ **`index=False`** prevents Pandas from saving the **row index** to the file.  

---

## **5. Handling Large CSV Files Efficiently**
Sometimes, CSV files are **huge** and can't fit into memory.

### **🔹 Reading Only a Few Rows**
```python
df = pd.read_csv("large_data.csv", nrows=1000)  # Read only first 1000 rows
```

### **🔹 Reading in Chunks**
```python
chunk_size = 50000  # Process 50,000 rows at a time
for chunk in pd.read_csv("large_data.csv", chunksize=chunk_size):
    print(chunk.shape)  # Process chunk by chunk
```
✅ **This is useful for large datasets** that don’t fit into RAM.  

---

## **6. Handling Different CSV Formats**
### **🔹 Changing Delimiters**
Some CSV files use **tabs (`\t`) or semicolons (`;`)** instead of commas.

```python
df = pd.read_csv("data.tsv", sep='\t')  # Read tab-separated file
```

### **🔹 Handling Missing Values While Reading**
```python
df = pd.read_csv("data.csv", na_values=["?", "N/A", "missing"])
```
✅ This replaces `?`, `N/A`, or `missing` with **NaN (Not a Number)**.  

---

## **7. Filtering and Modifying CSV Data**
### **🔹 Filtering Data**
```python
high_salary = df[df['Salary'] > 50000]  # Get rows where Salary > 50,000
```

### **🔹 Adding a New Column**
```python
df['Bonus'] = df['Salary'] * 0.10  # Add a 10% bonus column
```

### **🔹 Removing a Column**
```python
df.drop(columns=['Bonus'], inplace=True)  # Remove the "Bonus" column
```

---

## **8. Sorting and Grouping Data**
### **🔹 Sorting by a Column**
```python
df_sorted = df.sort_values(by='Salary', ascending=False)  # Highest salary first
```

### **🔹 Grouping and Aggregating Data**
```python
df_grouped = df.groupby('Department')['Salary'].mean()  # Average Salary per Department
```

---

## **9. Working with Dates in CSV Files**
If a CSV file contains **dates**, Pandas can convert them into a usable format.

### **🔹 Converting Date Columns**
```python
df['Date'] = pd.to_datetime(df['Date'])  # Convert to datetime format
```

### **🔹 Extracting Date Parts**
```python
df['Year'] = df['Date'].dt.year
df['Month'] = df['Date'].dt.month
```

---

## **10. Interview Summary (Key Takeaways)**
✅ **Use `pd.read_csv()` to load data, `df.to_csv()` to save it.**  
✅ **Always check data with `df.info()`, `df.shape()`, and `df.head()`.**  
✅ **Use `index=False` to avoid unnecessary columns while saving.**  
✅ **Handle missing data with `na_values`, `fillna()`, or `dropna()`.**  
✅ **For large files, use `chunksize` or `nrows` to optimize performance.**  
✅ **Convert dates using `pd.to_datetime()` for better time analysis.**  

---


# **Merging Data in Pandas (Beginner-Friendly Guide)**  

## **Why Do We Need Merging?**  
🔹 Often, **data is spread across multiple files** (like different CSVs).  
🔹 Instead of manually copying data, we can **merge (combine)** it efficiently using Pandas.  
🔹 This is useful in **real-world scenarios**, such as combining:  
   - **Employee records** (one table has names, another has salaries)  
   - **Sales data** (one table has products, another has sales figures)  
   - **Database-like operations** (joining tables like in SQL)  

---

## **1. Types of Merging (Joins) in Pandas**  
Pandas provides **4 main types of merging** (similar to SQL joins):  

| Merge Type  | Keeps Matching Rows? | Keeps Unmatched Rows? |
|-------------|----------------------|----------------------|
| **Inner Join**  | ✅ Yes  | ❌ No  |
| **Outer Join**  | ✅ Yes  | ✅ Yes (fills missing values with NaN) |
| **Left Join**   | ✅ Yes (all from left)  | ✅ Yes (only unmatched from right) |
| **Right Join**  | ✅ Yes (all from right) | ✅ Yes (only unmatched from left) |

### **How Do We Perform Merging in Pandas?**  
Pandas provides **`merge()`** to combine two DataFrames based on a **common column**.

---

## **2. Inner Join (Most Common)**
🔹 **Keeps only matching rows** (removes non-matching data).  
🔹 Example: We have two datasets – **Employees** and **Salaries**.

```python
import pandas as pd

# First DataFrame (Employee Details)
df1 = pd.DataFrame({
    'EmployeeID': [1, 2, 3, 4],
    'Name': ['Alice', 'Bob', 'Charlie', 'David']
})

# Second DataFrame (Salaries)
df2 = pd.DataFrame({
    'EmployeeID': [2, 3, 4, 5],
    'Salary': [50000, 60000, 70000, 80000]
})

# Perform Inner Join (Keeps only matching EmployeeID values)
merged_df = pd.merge(df1, df2, on='EmployeeID', how='inner')

print(merged_df)
```
**Output:**
```
   EmployeeID   Name  Salary
0          2    Bob   50000
1          3  Charlie 60000
2          4   David  70000
```
✅ **Only Employees 2, 3, and 4 exist in both tables, so they are kept.**  
❌ **Employee 1 (from `df1`) and Employee 5 (from `df2`) are removed.**  

---

## **3. Left Join (Keeps All from Left, Matches from Right)**
🔹 **Keeps all rows from the "left" DataFrame (`df1`)**.  
🔹 If no match is found in `df2`, it **fills `NaN`**.  

```python
merged_df = pd.merge(df1, df2, on='EmployeeID', how='left')
print(merged_df)
```
**Output:**
```
   EmployeeID   Name  Salary
0          1  Alice     NaN
1          2    Bob   50000
2          3  Charlie 60000
3          4   David  70000
```
✅ **All employees from `df1` are kept.**  
✅ **Matching salaries from `df2` are added.**  
❌ **Alice has no salary in `df2`, so it shows `NaN`.**  

---

## **4. Right Join (Keeps All from Right, Matches from Left)**
🔹 **Keeps all rows from `df2`**, and matches from `df1`.  
🔹 If no match is found in `df1`, it **fills `NaN`**.

```python
merged_df = pd.merge(df1, df2, on='EmployeeID', how='right')
print(merged_df)
```
**Output:**
```
   EmployeeID   Name  Salary
0          2    Bob   50000
1          3  Charlie 60000
2          4   David  70000
3          5     NaN   80000
```
✅ **All employees from `df2` are kept.**  
✅ **Matching names from `df1` are added.**  
❌ **Employee 5 has no name in `df1`, so it shows `NaN`.**  

---

## **5. Outer Join (Keeps Everything, Fills Missing with NaN)**
🔹 **Combines ALL records from both DataFrames.**  
🔹 **Fills `NaN` wherever there is no match.**  

```python
merged_df = pd.merge(df1, df2, on='EmployeeID', how='outer')
print(merged_df)
```
**Output:**
```
   EmployeeID   Name  Salary
0          1  Alice     NaN
1          2    Bob   50000
2          3  Charlie 60000
3          4   David  70000
4          5     NaN   80000
```
✅ **All employees from both tables are kept.**  
✅ **Unmatched values are filled with `NaN`.**  

---

## **6. Merging on Multiple Columns**
Sometimes, you may need to **merge on more than one column**.

```python
df1 = pd.DataFrame({
    'EmployeeID': [1, 2, 3],
    'Department': ['HR', 'IT', 'Finance'],
    'Name': ['Alice', 'Bob', 'Charlie']
})

df2 = pd.DataFrame({
    'EmployeeID': [1, 2, 3],
    'Department': ['HR', 'IT', 'Finance'],
    'Salary': [50000, 60000, 70000]
})

merged_df = pd.merge(df1, df2, on=['EmployeeID', 'Department'], how='inner')
print(merged_df)
```
✅ **Both `EmployeeID` and `Department` must match for merging.**  

---

## **7. Concatenating Data (Stacking Rows)**
🔹 If you have **two DataFrames with the same columns**, you can **stack them** on top of each other.

```python
df1 = pd.DataFrame({'EmployeeID': [1, 2], 'Name': ['Alice', 'Bob']})
df2 = pd.DataFrame({'EmployeeID': [3, 4], 'Name': ['Charlie', 'David']})

df_combined = pd.concat([df1, df2], axis=0)  # Combine row-wise
print(df_combined)
```
✅ **Stacks `df2` below `df1` like adding new rows.**  

---

## **8. Summary (How to Remember This?)**
Think of merging as **matching values in two tables**.  

| Type        | What It Does |
|-------------|-------------|
| **Inner Join**  | Keeps only matching rows (removes non-matching). |
| **Left Join**   | Keeps all from left, matches from right (fills missing with NaN). |
| **Right Join**  | Keeps all from right, matches from left (fills missing with NaN). |
| **Outer Join**  | Keeps all from both tables (fills missing with NaN). |

---

## **9. Interview Cheat Sheet**
✔ **Use `on='ColumnName'` to merge on a common column.**  
✔ **Use `how='inner'` for matching data only.**  
✔ **Use `how='left'` to keep all left-side data.**  
✔ **Use `how='outer'` to keep everything.**  
✔ **Use `concat()` to stack rows.**  

---
