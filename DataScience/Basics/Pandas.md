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
