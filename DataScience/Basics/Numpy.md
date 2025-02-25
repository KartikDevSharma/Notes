

#### **What is NumPy?**  
NumPy (Numerical Python) is a Python library used for working with numerical data. It provides powerful tools to store, manipulate, and perform mathematical operations on large datasets efficiently.  

Think of NumPy as an **upgrade to Python lists**—it allows you to store numbers in a better way and perform calculations much faster.  

#### **Why Use NumPy Instead of Lists?**  
Python lists are flexible, but they are slow when working with large amounts of data. NumPy arrays (**ndarrays**) are:  
✅ **Faster** – Uses less memory and runs operations quicker.  
✅ **More convenient** – Provides built-in functions for calculations like mean, sum, etc.  
✅ **Supports multi-dimensional arrays** – Unlike Python lists, it can handle matrices and higher-dimensional data.  

---

### **Basic NumPy Operations**  

#### **1. Creating a NumPy Array**  
To use NumPy, first, install and import it:  
```python
pip install numpy  # Install NumPy if not installed
import numpy as np  # Import NumPy
```

Now, create a simple NumPy array:  
```python
arr = np.array([1, 2, 3, 4, 5])  
print(arr)  # Output: [1 2 3 4 5]
```
🔹 This looks like a Python list, but it’s actually a NumPy **array**.

#### **2. Checking Array Properties**  
```python
print(arr.shape)  # Shows the dimensions (1D array with 5 elements)
print(arr.dtype)  # Shows the data type (e.g., int32 or float64)
print(arr.size)   # Total number of elements (5 in this case)
```

---

### **Types of NumPy Arrays**
NumPy supports different types of arrays:  
1️⃣ **1D array** (Vector) → `[1, 2, 3]`  
2️⃣ **2D array** (Matrix) → `[[1, 2], [3, 4]]`  
3️⃣ **3D array** (Tensor) → `[[[1, 2], [3, 4]], [[5, 6], [7, 8]]]`  

Example of a **2D array (matrix)**:  
```python
matrix = np.array([[1, 2, 3], [4, 5, 6]])
print(matrix)
# Output:
# [[1 2 3]
#  [4 5 6]]
```

---

### **3. Useful NumPy Functions**  

✅ **Creating arrays with default values**  
```python
np.zeros((3, 3))  # Creates a 3x3 matrix filled with 0s
np.ones((2, 2))   # Creates a 2x2 matrix filled with 1s
np.eye(3)         # Creates a 3x3 Identity matrix
```

✅ **Generating sequences**  
```python
np.arange(1, 10, 2)  # Output: [1 3 5 7 9] (Start=1, Stop=10, Step=2)
np.linspace(0, 1, 5)  # Output: [0.   0.25 0.5  0.75 1. ] (5 values evenly spaced)
```

✅ **Reshaping an array**  
```python
arr = np.array([1, 2, 3, 4, 5, 6])
reshaped = arr.reshape(2, 3)  # Changes shape to 2 rows, 3 columns
print(reshaped)
# Output:
# [[1 2 3]
#  [4 5 6]]
```

✅ **Mathematical operations**  
NumPy makes calculations super easy:  
```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(a + b)  # Output: [5 7 9]  (Element-wise addition)
print(a * b)  # Output: [ 4 10 18] (Element-wise multiplication)
print(np.sqrt(a))  # Square root of each element
print(np.mean(a))  # Mean (average)
print(np.sum(a))   # Sum of all elements
```

---

### **4. Indexing & Slicing in NumPy**  
Just like Python lists, you can access specific elements in NumPy arrays.  
```python
arr = np.array([10, 20, 30, 40, 50])
print(arr[0])    # First element → 10
print(arr[-1])   # Last element → 50
print(arr[1:4])  # Slice from index 1 to 3 → [20 30 40]
```

For **2D arrays**, indexing works like this:  
```python
matrix = np.array([[1, 2, 3], [4, 5, 6]])
print(matrix[0, 1])  # Element at row 0, column 1 → 2
print(matrix[:, 1])  # All rows, column 1 → [2 5]
```

---

### **5. Broadcasting (Different Sized Arrays)**  
NumPy allows operations between different-sized arrays **without using loops**.  
```python
arr = np.array([1, 2, 3])
print(arr + 5)  # Output: [6 7 8] (Adds 5 to each element)
```
🔹 This is called **broadcasting**, where NumPy automatically expands the smaller array.

---

### **6. Reading & Writing Files**  
✅ **Saving and Loading NumPy Arrays**  
```python
np.save("data.npy", arr)  # Save array to a file
loaded_arr = np.load("data.npy")  # Load array from a file
```

✅ **Reading CSV files (like Excel data)**  
```python
data = np.genfromtxt('file.csv', delimiter=',')
print(data)
```

---

### **Interview Tips: Common NumPy Questions**  
1️⃣ **What is NumPy, and why is it useful?**  
➡ NumPy is a library for fast numerical computations, making Python lists more efficient.  

2️⃣ **Difference between Python lists and NumPy arrays?**  
➡ NumPy arrays are **faster, consume less memory, and support multi-dimensional operations**.  

3️⃣ **How do you create a NumPy array?**  
➡ Using `np.array([1, 2, 3])`.  

4️⃣ **What is broadcasting?**  
➡ Automatically adjusting different-sized arrays for operations (e.g., `[1, 2, 3] + 5 → [6, 7, 8]`).  

5️⃣ **How to create an array filled with ones?**  
➡ `np.ones((3,3))` creates a 3x3 matrix filled with ones.  

---


### **Indexing with a Mask in NumPy (Boolean Masking)**  

**What is Masked Indexing?**  
Masked indexing (also called **Boolean masking**) allows you to filter or extract elements from a NumPy array **based on a condition**. Instead of using index positions, you use a **Boolean mask** (an array of `True` or `False` values).  

This technique is **very powerful** for filtering and modifying data efficiently.  

---

## **1. Basic Masking Example**
```python
import numpy as np

arr = np.array([10, 20, 30, 40, 50])
mask = arr > 25  # Create a boolean mask (True where value > 25)

print(mask)  
# Output: [False False  True  True  True]

print(arr[mask])  
# Output: [30 40 50]  (Only values greater than 25)
```
🔹 **How it works?**  
- `arr > 25` creates a Boolean mask: `[False, False, True, True, True]`  
- Using `arr[mask]` selects only `True` values from `arr`.  

---

## **2. Using Masking with Different Conditions**  

✅ **Find even numbers**  
```python
arr = np.array([1, 2, 3, 4, 5, 6])
mask = arr % 2 == 0  # Mask for even numbers
print(arr[mask])  # Output: [2 4 6]
```

✅ **Find numbers in a specific range**  
```python
arr = np.array([10, 20, 30, 40, 50])
mask = (arr > 15) & (arr < 45)  # Find numbers between 15 and 45
print(arr[mask])  # Output: [20 30 40]
```
🔹 **Note:**  
- Use `&` (AND) instead of `and`.  
- Use `|` (OR) instead of `or`.  

✅ **Find negative numbers**  
```python
arr = np.array([-5, 10, -15, 20, 25])
mask = arr < 0
print(arr[mask])  # Output: [-5 -15]
```

---

## **3. Modifying Data Using Masking**  
You can use masked indexing **not just to extract values but also to modify them**.

✅ **Set all negative values to zero**  
```python
arr = np.array([-10, 5, -3, 8, -1])
arr[arr < 0] = 0  # Replace all negative numbers with 0
print(arr)  # Output: [0 5 0 8 0]
```

✅ **Increase all values greater than 10 by 100**  
```python
arr = np.array([5, 12, 7, 20])
arr[arr > 10] += 100
print(arr)  # Output: [  5 112   7 120]
```

---

## **4. Masking in Multi-Dimensional Arrays**  

✅ **Find elements greater than 10 in a 2D array**  
```python
arr = np.array([[5, 15, 25], [2, 8, 30]])
mask = arr > 10
print(arr[mask])  # Output: [15 25 30]
```
🔹 The result is **a 1D array** of matching values.

✅ **Set all values < 10 to zero in a 2D array**  
```python
arr[arr < 10] = 0
print(arr)
# Output:
# [[ 0 15 25]
#  [ 0  0 30]]
```

---

## **5. Using `np.where()` for Masking**
`np.where(condition, value_if_true, value_if_false)` is useful for replacing values.  
```python
arr = np.array([10, 20, 30, 40])
new_arr = np.where(arr > 20, 1, 0)  # Replace values > 20 with 1, others with 0
print(new_arr)  # Output: [0 0 1 1]
```

---

## **6. Masking with NaN (Missing Values)**
✅ **Replace NaN values with 0**  
```python
arr = np.array([1, np.nan, 3, np.nan, 5])
arr[np.isnan(arr)] = 0  # Replace NaN with 0
print(arr)  # Output: [1. 0. 3. 0. 5.]
```

✅ **Filter out NaN values**  
```python
cleaned_arr = arr[~np.isnan(arr)]  # Remove NaN values
print(cleaned_arr)  # Output: [1. 3. 5.]
```

---

## **Interview Tips (Common Questions)**  
1️⃣ **What is masked indexing in NumPy?**  
➡ It is a way to filter or modify arrays using Boolean conditions.  

2️⃣ **How to find values greater than 10 in an array?**  
➡ `arr[arr > 10]`  

3️⃣ **How to replace negative values with zero?**  
➡ `arr[arr < 0] = 0`  

4️⃣ **Difference between masked indexing and `np.where()`?**  
➡ **Masked indexing** directly extracts or modifies elements, while `np.where()` allows conditional replacements.

---

### **Summary**
✅ **Masked indexing** is a powerful tool for filtering and modifying arrays.  
✅ **Boolean masks** allow selection based on conditions.  
✅ **Works on multi-dimensional arrays too.**  
✅ **`np.where()` is useful for conditional replacements.**  

---

# **Numerical Operations on NumPy Arrays**  

NumPy provides **fast, efficient, and vectorized** numerical operations on arrays. Instead of using loops (which are slow), NumPy allows **element-wise** and **aggregate** operations on entire arrays at once.  

---

## **1. Element-wise Arithmetic Operations**  
These operations apply **to each element** of the array automatically.

```python
import numpy as np

arr1 = np.array([1, 2, 3, 4])
arr2 = np.array([10, 20, 30, 40])

# Addition
print(arr1 + arr2)  # Output: [11 22 33 44]

# Subtraction
print(arr2 - arr1)  # Output: [ 9 18 27 36]

# Multiplication
print(arr1 * arr2)  # Output: [ 10  40  90 160]

# Division
print(arr2 / arr1)  # Output: [10. 10. 10. 10.]

# Power
print(arr1 ** 2)  # Output: [ 1  4  9 16]
```
🔹 **No loops needed! Operations are performed on entire arrays at once.**  

---

## **2. Scalar Operations**  
When you apply an operation between an array and a **single number (scalar)**, NumPy **broadcasts** the scalar to all elements.

```python
arr = np.array([1, 2, 3, 4])

print(arr + 10)  # Output: [11 12 13 14] (Adds 10 to each element)
print(arr * 2)   # Output: [2 4 6 8] (Multiplies each element by 2)
print(arr / 2)   # Output: [0.5 1.  1.5 2. ] (Divides each element by 2)
```

---

## **3. Aggregate Functions (Sum, Mean, Max, etc.)**
NumPy provides **built-in functions** to compute **summary statistics** on arrays.

```python
arr = np.array([1, 2, 3, 4, 5])

print(np.sum(arr))   # Output: 15 (Sum of all elements)
print(np.mean(arr))  # Output: 3.0 (Mean/Average)
print(np.max(arr))   # Output: 5 (Maximum value)
print(np.min(arr))   # Output: 1 (Minimum value)
print(np.prod(arr))  # Output: 120 (Product of all elements)
print(np.std(arr))   # Output: 1.414 (Standard deviation)
```

✅ **Works on multi-dimensional arrays too!**  

```python
arr2D = np.array([[1, 2, 3], [4, 5, 6]])

print(np.sum(arr2D, axis=0))  # Sum along columns → Output: [5 7 9]
print(np.sum(arr2D, axis=1))  # Sum along rows    → Output: [ 6 15]
```
🔹 `axis=0` → operates **column-wise**  
🔹 `axis=1` → operates **row-wise**  

---

## **4. Rounding and Trigonometric Operations**
NumPy provides functions for rounding and trigonometric operations.

```python
arr = np.array([3.14, 1.67, -2.89])

# Rounding
print(np.round(arr))  # Output: [ 3.  2. -3.]
print(np.floor(arr))  # Output: [ 3.  1. -3.] (Round down)
print(np.ceil(arr))   # Output: [ 4.  2. -2.] (Round up)
```

### **Trigonometric Functions**
```python
angles = np.array([0, 30, 45, 60, 90])  # Degrees
radians = np.radians(angles)  # Convert to radians

print(np.sin(radians))  # Sine values
print(np.cos(radians))  # Cosine values
print(np.tan(radians))  # Tangent values
```

---

## **5. Logarithmic and Exponential Functions**
```python
arr = np.array([1, 2, 10, 100])

print(np.log(arr))   # Natural log (base e)
print(np.log2(arr))  # Log base 2
print(np.log10(arr)) # Log base 10
print(np.exp(arr))   # Exponential (e^x)
```

---

## **6. Modulo and Absolute Value**
```python
arr = np.array([-10, 20, -30, 40])

print(np.abs(arr))   # Output: [10 20 30 40] (Absolute values)
print(np.mod(arr, 3))  # Output: [2 2 0 1] (Modulo 3)
```

---

## **7. Matrix Operations**
NumPy allows **matrix operations** like dot product and transpose.

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

# Matrix multiplication (dot product)
print(np.dot(A, B))  
# Output:
# [[19 22]
#  [43 50]]

# Transpose of a matrix
print(A.T)  
# Output:
# [[1 3]
#  [2 4]]
```

---

## **Interview Summary (Important Points)**
1️⃣ **NumPy performs element-wise operations efficiently.**  
2️⃣ **Scalar operations get broadcasted across arrays.**  
3️⃣ **Use built-in aggregate functions (`sum`, `mean`, `max`, etc.).**  
4️⃣ **NumPy supports rounding, trigonometric, log, and exponential functions.**  
5️⃣ **Matrix operations like dot product and transpose are optimized.**  


 ---

