

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

