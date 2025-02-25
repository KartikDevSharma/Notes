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

