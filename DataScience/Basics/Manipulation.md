# **Data Manipulation with Pandas and NumPy (Beginner-Friendly Guide)**  

## **Why Learn Data Manipulation?**  
Data in its raw form is often **messy, incomplete, or unstructured**. Before using it for **analysis or machine learning**, we need to **clean, transform, and structure it** properly.  
🔹 **NumPy** helps with numerical operations on large datasets.  
🔹 **Pandas** makes **tabular data handling** easy and efficient.  

---

## **1. NumPy for Data Manipulation**
NumPy is useful when working with large **numerical datasets** because it provides:
✅ **Faster** operations than Python lists  
✅ **Element-wise operations** for quick computations  
✅ **Broadcasting** for handling different array sizes  

### **Creating and Modifying Arrays**
```python
import numpy as np

arr = np.array([10, 20, 30, 40])
print(arr)  # Output: [10 20 30 40]
```
🔹 **Changing Values in an Array**
```python
arr[1] = 50  # Change 20 to 50
print(arr)  # Output: [10 50 30 40]
```
🔹 **Adding and Removing Elements**
```python
arr = np.append(arr, [60, 70])  # Add values at the end
arr = np.delete(arr, 0)  # Remove first element
print(arr)  # Output: [50 30 40 60 70]
```
🔹 **Filtering Data with Conditions**
```python
filtered = arr[arr > 40]  # Get only values > 40
print(filtered)  # Output: [50 60 70]
```

---

## **2. Pandas for Data Manipulation**
Pandas is used for working with **structured data** (tables, CSV files, databases).  
It provides **powerful tools** to clean, filter, and modify data.

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

---

## **3. Common Data Manipulation Tasks in Pandas**
### **(a) Adding, Updating, and Removing Data**
🔹 **Adding a New Column**
```python
df['Bonus'] = df['Salary'] * 0.10  # 10% bonus for each person
```
🔹 **Updating a Column**
```python
df['Age'] = df['Age'] + 1  # Increase everyone's age by 1
```
🔹 **Removing Columns**
```python
df.drop('Bonus', axis=1, inplace=True)  # Removes the "Bonus" column
```
🔹 **Removing Rows**
```python
df.drop(1, axis=0, inplace=True)  # Removes row at index 1 (Bob)
```

---

## **4. Filtering and Selecting Data**
### **(a) Selecting Specific Columns**
```python
print(df[['Name', 'Salary']])  # Select only "Name" and "Salary" columns
```
### **(b) Filtering Data Based on Conditions**
```python
high_salary = df[df['Salary'] > 55000]  # Get employees earning more than 55K
```
### **(c) Selecting Rows with `loc` and `iloc`**
```python
print(df.loc[0])  # Select row with index 0 (Alice)
print(df.iloc[1])  # Select second row using position-based index
```

---

## **5. Handling Missing Data**
Real-world data often has missing values. Pandas provides easy ways to handle them.

🔹 **Checking for Missing Values**
```python
print(df.isnull().sum())  # Counts missing values per column
```
🔹 **Filling Missing Values**
```python
df.fillna(0, inplace=True)  # Replace NaN with 0
```
🔹 **Removing Rows with Missing Values**
```python
df.dropna(inplace=True)  # Drop rows with missing values
```

---

## **6. Sorting and Rearranging Data**
🔹 **Sorting by Column Values**
```python
df_sorted = df.sort_values(by='Salary', ascending=False)  # Highest Salary first
```
🔹 **Reordering Columns**
```python
df = df[['Name', 'Salary', 'Age']]  # Change column order
```

---

## **7. Grouping and Aggregation**
🔹 **Grouping Data by a Column**
```python
df_grouped = df.groupby('Age').mean()  # Average Salary grouped by Age
```
🔹 **Applying Multiple Aggregations**
```python
df_agg = df.groupby('Age').agg({'Salary': ['mean', 'max', 'min']})
```

---

## **8. Merging and Joining Data**
Often, we work with multiple datasets that need to be combined.

🔹 **Merging Two DataFrames**
```python
df1 = pd.DataFrame({'ID': [1, 2], 'Name': ['Alice', 'Bob']})
df2 = pd.DataFrame({'ID': [1, 2], 'Salary': [50000, 60000]})

df_merged = pd.merge(df1, df2, on='ID')  # Merge using common "ID" column
```
🔹 **Concatenating Rows**
```python
df_new = pd.concat([df1, df2], axis=0)  # Stack data vertically
```

---

## **9. Working with Time-Series Data**
🔹 **Converting Strings to Dates**
```python
df['Date'] = pd.to_datetime(df['Date'])
```
🔹 **Extracting Date Parts**
```python
df['Year'] = df['Date'].dt.year
df['Month'] = df['Date'].dt.month
```

---

## **10. Combining Pandas and NumPy**
Pandas and NumPy work **together** for complex transformations.

🔹 **Using NumPy for Conditional Operations**
```python
df['Category'] = np.where(df['Salary'] > 55000, 'High', 'Low')
```
🔹 **Applying NumPy Functions on Pandas Columns**
```python
df['Log_Salary'] = np.log(df['Salary'])  # Compute log of Salary
```

---

## **Interview Summary (Key Takeaways)**
✅ **NumPy is great for numerical operations, Pandas for structured data.**  
✅ **Use `axis=0` for rows, `axis=1` for columns (e.g., `drop()`).**  
✅ **Filtering is easy using conditions like `df[df['Salary'] > 50000]`.**  
✅ **Handle missing data with `fillna()` or `dropna()`.**  
✅ **Use `merge()` for combining DataFrames based on a key.**  
✅ **Use NumPy with Pandas for efficient calculations (`np.log()`, `np.where()`).**  

