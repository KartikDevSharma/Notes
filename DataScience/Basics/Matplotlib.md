# **📊 Data Visualization with Matplotlib (Absolute Beginner Guide) 📊**  

## **What is Data Visualization?**  
🔹 When you have a bunch of numbers in a table, it's **hard to understand** trends.  
🔹 **Graphs and charts** make data **easy to see and interpret**.  
🔹 **Matplotlib** is a Python library that helps create graphs.  

---

## **1️⃣ First Steps: Install and Import Matplotlib**  
📌 **Matplotlib** comes pre-installed in many Python setups, but if needed, install it with:  
```
pip install matplotlib
```

### **Importing Matplotlib**
```python
import matplotlib.pyplot as plt  # "pyplot" is used for plotting
```
✅ `plt` is a shortcut, so we don’t have to type `matplotlib.pyplot` every time.

---

## **2️⃣ Creating a Basic Line Chart**  
**🎯 Goal:** Plot a simple line graph.  

### **Example Data (Sales Over 5 Months)**  
| Month  | Sales (in $1000s) |
|--------|------------------|
| Jan    | 10               |
| Feb    | 15               |
| Mar    | 7                |
| Apr    | 12               |
| May    | 18               |

### **Code to Plot the Graph**
```python
import matplotlib.pyplot as plt

# Data
months = ["Jan", "Feb", "Mar", "Apr", "May"]
sales = [10, 15, 7, 12, 18]

# Create the plot
plt.plot(months, sales)

# Add labels
plt.xlabel("Months")
plt.ylabel("Sales (in $1000s)")
plt.title("Sales Over 5 Months")

# Show the graph
plt.show()
```
✅ **What’s Happening?**  
1. 📌 `plt.plot(x, y)` → Creates a line graph with `x = months` and `y = sales`.  
2. 🏷️ `plt.xlabel()` and `plt.ylabel()` → Label the axes.  
3. 🏆 `plt.title()` → Adds a title to the graph.  
4. 👀 `plt.show()` → Displays the graph.  

**🔹 Output:** A line graph showing sales trends over 5 months.

---

## **3️⃣ Creating a Bar Chart**  
**🎯 Goal:** Show sales using bars instead of a line.  

```python
plt.bar(months, sales, color='blue')  # Bar graph with blue bars
plt.xlabel("Months")
plt.ylabel("Sales (in $1000s)")
plt.title("Sales Over 5 Months")
plt.show()
```
✅ **Key Difference:**  
- **`plt.bar()`** instead of `plt.plot()`.  
- Shows bars instead of a line.  

📊 **When to Use a Bar Chart?**  
🔹 **Comparing different values** (e.g., sales in different months).  
🔹 **Categorical data** (e.g., sales in different cities).  

---

## **4️⃣ Creating a Scatter Plot**  
📌 **Use Case:** When you want to **see relationships** between two things.  
**Example:** Relationship between advertising budget and sales.

```python
ad_budget = [2, 4, 6, 8, 10]  # Advertising in $1000s
sales = [7, 10, 15, 18, 22]   # Sales in $1000s

plt.scatter(ad_budget, sales, color="red")  # Scatter plot with red dots
plt.xlabel("Ad Budget ($1000s)")
plt.ylabel("Sales ($1000s)")
plt.title("Ad Budget vs Sales")
plt.show()
```
✅ **Key Difference:**  
- **`plt.scatter()`** → Uses dots instead of lines or bars.  
- Great for **finding patterns** between two numerical values.  

---

## **5️⃣ Creating a Pie Chart**  
📌 **Use Case:** When you want to **show proportions** (percentages).  
**Example:** Market share of 4 companies.

```python
companies = ["A", "B", "C", "D"]
market_share = [40, 30, 20, 10]  # Percentages

plt.pie(market_share, labels=companies, autopct="%1.1f%%", colors=['blue', 'red', 'green', 'orange'])
plt.title("Market Share of Companies")
plt.show()
```
✅ **What’s Happening?**  
- **`plt.pie(values, labels=..., autopct="%.1f%%")`** → Creates a pie chart.  
- **`colors`** → Changes colors of slices.  

📊 **When to Use a Pie Chart?**  
🔹 **When you want to show parts of a whole** (e.g., percentage of total sales).  

---

## **6️⃣ Customizing Your Graphs**  
📌 **Make graphs easier to read by adding details.**  

🔹 **Change Line Color & Style**  
```python
plt.plot(months, sales, color="red", linestyle="dashed", marker="o")
```
🔹 **Add a Grid**  
```python
plt.grid(True)
```
🔹 **Change Figure Size**  
```python
plt.figure(figsize=(8,5))  # Width=8, Height=5
```

---

## **7️⃣ Multiple Graphs in One Figure**  
📌 **Use `plt.subplot()` to create multiple graphs together.**  

```python
plt.figure(figsize=(10,5))  # Set figure size

# First plot (Line Chart)
plt.subplot(1,2,1)  # (rows, columns, plot number)
plt.plot(months, sales, color='blue')
plt.title("Sales Line Chart")

# Second plot (Bar Chart)
plt.subplot(1,2,2)
plt.bar(months, sales, color='red')
plt.title("Sales Bar Chart")

plt.tight_layout()  # Adjust layout to prevent overlap
plt.show()
```
✅ **What’s Happening?**  
- **`plt.subplot(1,2,1)`** → 1 row, 2 columns, 1st plot.  
- **`plt.subplot(1,2,2)`** → 2nd plot in the same row.  

---

## **💡 Summary Table: Which Chart to Use?**  
| **Chart Type** | **Use When...** |
|---------------|----------------|
| **Line Chart** (`plt.plot()`) | Showing trends over time (e.g., monthly sales). |
| **Bar Chart** (`plt.bar()`) | Comparing different values (e.g., sales in different cities). |
| **Scatter Plot** (`plt.scatter()`) | Checking relationship between two things (e.g., advertising vs sales). |
| **Pie Chart** (`plt.pie()`) | Showing proportions (e.g., market share). |

---

## **🎯 How to Remember All This?**  
1. **Think About Your Goal:**  
   - **Trend?** → Use a **Line Chart**.  
   - **Comparison?** → Use a **Bar Chart**.  
   - **Relationship?** → Use a **Scatter Plot**.  
   - **Proportion?** → Use a **Pie Chart**.  

2. **Just Remember These Five Functions:**  
   ```python
   plt.plot()      # Line Chart
   plt.bar()       # Bar Chart
   plt.scatter()   # Scatter Plot
   plt.pie()       # Pie Chart
   plt.show()      # Display Graph
   ```

3. **Practice!** Try creating a simple plot every day.  

---

# **📊 Multiple Graphs in One Figure (Absolute Beginner Guide)**  

## **What Does "Multiple Graphs in One Figure" Mean?**  
🔹 Sometimes, you need to compare different graphs **side by side** instead of making separate figures.  
🔹 Matplotlib lets you **put multiple graphs in the same window** using **`plt.subplot()`**.  

✅ **This is useful when you want to:**  
- Compare **two different data trends** at once.  
- Show **different visualizations** of the same data (e.g., **Line Chart vs. Bar Chart**).  
- Save space by **grouping multiple plots together**.  

---

## **1️⃣ The Basic Idea: `plt.subplot()`**
`plt.subplot(rows, columns, plot_number)`

📌 **Breaking it Down:**  
1. **Rows (`rows`)** → How many rows of graphs do you want?  
2. **Columns (`columns`)** → How many columns of graphs do you want?  
3. **Plot Number (`plot_number`)** → Which graph are you working on?  

👉 Think of it as **a grid of plots** where you "fill" each slot one by one.

---

## **2️⃣ Simple Example: Two Graphs (One Row, Two Columns)**  
**🎯 Goal:** Show **sales data** using both **Line Chart and Bar Chart** in the same figure.

```python
import matplotlib.pyplot as plt

# Data
months = ["Jan", "Feb", "Mar", "Apr", "May"]
sales = [10, 15, 7, 12, 18]

plt.figure(figsize=(10, 5))  # Set figure size

# First Plot (Line Chart)
plt.subplot(1, 2, 1)  # 1 row, 2 columns, this is the first plot
plt.plot(months, sales, color='blue', marker='o')
plt.title("Sales Trend (Line Chart)")
plt.xlabel("Months")
plt.ylabel("Sales ($1000s)")

# Second Plot (Bar Chart)
plt.subplot(1, 2, 2)  # 1 row, 2 columns, this is the second plot
plt.bar(months, sales, color='red')
plt.title("Sales Data (Bar Chart)")
plt.xlabel("Months")
plt.ylabel("Sales ($1000s)")

plt.tight_layout()  # Adjust layout to prevent overlap
plt.show()
```

---

### **💡 What’s Happening Here?**
✅ `plt.figure(figsize=(10,5))` → Sets the **size of the whole figure**.  
✅ `plt.subplot(1, 2, 1)` → **1 row, 2 columns**, this is **plot 1**.  
✅ `plt.subplot(1, 2, 2)` → **1 row, 2 columns**, this is **plot 2**.  
✅ `plt.tight_layout()` → **Fixes overlapping labels automatically.**  
✅ `plt.show()` → **Displays everything in one window!**  

---

## **3️⃣ Arranging Graphs in Rows and Columns**
Sometimes, you need more than **two** graphs. You can use **multiple rows and columns**.

---

### **Example: 2 Rows, 2 Columns (4 Graphs)**
```python
import matplotlib.pyplot as plt

# Data
x = [1, 2, 3, 4, 5]
y1 = [10, 20, 30, 40, 50]
y2 = [5, 15, 25, 35, 45]
y3 = [2, 4, 6, 8, 10]
y4 = [3, 6, 9, 12, 15]

plt.figure(figsize=(10, 8))  # Set figure size

# First plot (Line Chart)
plt.subplot(2, 2, 1)  # 2 rows, 2 columns, 1st plot
plt.plot(x, y1, color='blue')
plt.title("Plot 1: Line Chart")

# Second plot (Bar Chart)
plt.subplot(2, 2, 2)  # 2 rows, 2 columns, 2nd plot
plt.bar(x, y2, color='green')
plt.title("Plot 2: Bar Chart")

# Third plot (Scatter Plot)
plt.subplot(2, 2, 3)  # 2 rows, 2 columns, 3rd plot
plt.scatter(x, y3, color='red')
plt.title("Plot 3: Scatter Plot")

# Fourth plot (Histogram)
plt.subplot(2, 2, 4)  # 2 rows, 2 columns, 4th plot
plt.hist(y4, bins=5, color='purple')
plt.title("Plot 4: Histogram")

plt.tight_layout()
plt.show()
```

---

### **💡 What’s Happening Here?**
✅ `plt.subplot(2, 2, 1)` → **1st plot in a 2x2 grid**.  
✅ `plt.subplot(2, 2, 2)` → **2nd plot in a 2x2 grid**.  
✅ `plt.subplot(2, 2, 3)` → **3rd plot in a 2x2 grid**.  
✅ `plt.subplot(2, 2, 4)` → **4th plot in a 2x2 grid**.  
✅ **Each graph has a different type (Line, Bar, Scatter, Histogram).**  

🔹 **This creates a 2x2 grid of graphs like this:**  
```
[ Plot 1 ]  [ Plot 2 ]
[ Plot 3 ]  [ Plot 4 ]
```

---

## **4️⃣ Adjusting Spacing Between Graphs**
🔹 If graphs **overlap**, use `plt.tight_layout()`.  
🔹 If you want **more control**, use `plt.subplots_adjust()`.  

```python
plt.subplots_adjust(left=0.1, right=0.9, top=0.9, bottom=0.1, wspace=0.3, hspace=0.5)
```
✅ **`wspace` (width space)** → Adds space between columns.  
✅ **`hspace` (height space)** → Adds space between rows.  

---

## **5️⃣ Using `plt.subplots()` Instead of `plt.subplot()`**
🔹 `plt.subplots()` is a **better alternative** to `plt.subplot()` because it **returns figure & axes** for more flexibility.

```python
fig, axes = plt.subplots(2, 2, figsize=(10, 8))

# First plot
axes[0, 0].plot(x, y1, color='blue')
axes[0, 0].set_title("Plot 1: Line Chart")

# Second plot
axes[0, 1].bar(x, y2, color='green')
axes[0, 1].set_title("Plot 2: Bar Chart")

# Third plot
axes[1, 0].scatter(x, y3, color='red')
axes[1, 0].set_title("Plot 3: Scatter Plot")

# Fourth plot
axes[1, 1].hist(y4, bins=5, color='purple')
axes[1, 1].set_title("Plot 4: Histogram")

plt.tight_layout()
plt.show()
```
✅ This method makes it **easier to modify each graph individually**.

---

## **💡 Summary: How to Remember This?**
1️⃣ **Use `plt.subplot(rows, columns, plot_number)` to position each graph.**  
2️⃣ **Always use `plt.tight_layout()` to fix overlapping issues.**  
3️⃣ **Use `plt.subplots()` if you need more control.**  
4️⃣ **Use `plt.subplots_adjust()` if you want to fine-tune spacing.**  
5️⃣ **Practice!** Start by making 2 plots, then try 4.  

---

---

# 📄 Plotting from CSV Files using Matplotlib – Beginner Friendly Guide

## 🧠 Why Plot from a CSV?

In real-world data science, data is **rarely hardcoded**. It's usually stored in external files like **CSV (Comma Separated Values)**.

Instead of typing values manually, we:
- ✅ Load the CSV using **Pandas**
- ✅ Extract the columns we want
- ✅ Plot them using **Matplotlib**

---

## 📦 What You’ll Need

```python
import pandas as pd       # For reading the CSV
import matplotlib.pyplot as plt  # For plotting
```

---

## 📁 Example CSV File (Let’s assume `data.csv` looks like this):

| Day   | Temperature | Humidity |
|-------|-------------|----------|
| Mon   | 30          | 60       |
| Tue   | 32          | 65       |
| Wed   | 34          | 55       |
| Thu   | 33          | 58       |
| Fri   | 31          | 62       |

---

## 🔰 Step-by-Step Code to Plot

```python
import pandas as pd
import matplotlib.pyplot as plt

# Step 1: Read the CSV file
data = pd.read_csv("data.csv")

# Step 2: Access the columns you want
days = data["Day"]
temp = data["Temperature"]
humidity = data["Humidity"]

# Step 3: Plot temperature and humidity
plt.plot(days, temp, marker='o', label='Temperature')
plt.plot(days, humidity, marker='s', label='Humidity')

# Step 4: Customize the plot
plt.title("Weather Data")
plt.xlabel("Day")
plt.ylabel("Value")
plt.legend()
plt.grid(True)

# Step 5: Show it
plt.show()
```

---

## 🧠 What’s Happening?

| Step | Description |
|------|-------------|
| `pd.read_csv()` | Reads the CSV into a **DataFrame** (like a table) |
| `data["Column"]` | Picks one specific column |
| `plt.plot()` | Plots that column vs another |
| `.legend()` | Adds labels for clarity |
| `.show()` | Displays the plot |

---

## 💡 Real-World Use Cases

| CSV Content               | What You Can Plot                         |
|---------------------------|-------------------------------------------|
| Stock prices              | Date vs. Price                            |
| Website analytics         | Date vs. Visitors                         |
| Sensor readings (IoT)     | Time vs. Sensor Values                    |
| Sales data                | Product vs. Revenue/Quantity              |

---

## ⚠️ Common Mistakes to Avoid

| Mistake | Fix |
|--------|-----|
| File not found | Make sure the CSV is in the **same folder** or use the **full path** |
| Column name typo | Use `print(data.columns)` to double-check column names |
| Non-numeric data | Only **numeric columns** can be plotted on Y-axis |

---

## 🗣️ Interview Tip – How to Explain It

> “In real projects, I rarely hardcode values. I use `pandas` to load CSV files and then extract columns I want to analyze. With Matplotlib, I can quickly visualize data trends like sales over time, sensor patterns, or website traffic. I always make sure to add labels and legends for clarity.”

---

## ✅ Summary

- Use `pandas` to load data from `.csv` files
- Access columns directly using `data['ColumnName']`
- Use `plt.plot()` (or other plot types) to visualize
- Add labels, legends, and grids for a clean look

---


You already saw that we use `pandas` to read CSVs and get data into a **DataFrame**. The cool thing is:  
> **You can plot directly from the DataFrame itself!**

---

# 🧾 Plotting using a Pandas DataFrame (Beginner Friendly)

## 🔧 Step 1: Import Your Tools

```python
import pandas as pd
import matplotlib.pyplot as plt
```

---

## 📁 Sample DataFrame

Let’s use this simple dataset:

```python
data = {
    'Day': ['Mon', 'Tue', 'Wed', 'Thu', 'Fri'],
    'Temperature': [30, 32, 34, 33, 31],
    'Humidity': [60, 65, 55, 58, 62]
}

df = pd.DataFrame(data)
print(df)
```

| Day | Temperature | Humidity |
|-----|-------------|----------|
| Mon | 30          | 60       |
| Tue | 32          | 65       |
| Wed | 34          | 55       |
| Thu | 33          | 58       |
| Fri | 31          | 62       |

---

## 📊 Plotting Directly from the DataFrame

### ✅ Line Plot
```python
df.plot(x='Day', y='Temperature', kind='line', marker='o')
plt.title("Temperature Over Days")
plt.ylabel("Temperature (°C)")
plt.grid(True)
plt.show()
```

✅ **Explanation:**
- `df.plot(...)` is a shortcut to Matplotlib.
- `x='Day'` uses the “Day” column as X-axis.
- `y='Temperature'` uses the “Temperature” column as Y-axis.
- `kind='line'` tells it to draw a line chart.
- `marker='o'` puts dots on each point.

---

## 🪄 Plotting Multiple Columns Together

You can plot **both temperature and humidity** on the same graph:

```python
df.plot(x='Day', y=['Temperature', 'Humidity'], kind='line', marker='o')
plt.title("Temperature and Humidity Over Days")
plt.ylabel("Values")
plt.grid(True)
plt.show()
```

This is super useful when you want to **compare trends** in two variables.

---

## 📊 Other Plot Types You Can Use

| `kind=`    | Chart Type      | Use Case Example                     |
|------------|------------------|-------------------------------------|
| `'line'`   | Line chart       | Trends over time                    |
| `'bar'`    | Vertical bars    | Comparing values (e.g., revenue)    |
| `'barh'`   | Horizontal bars  | Comparing long category names       |
| `'hist'`   | Histogram        | Distribution of values (e.g., age)  |
| `'box'`    | Box plot         | Summary statistics (median, IQR)    |
| `'scatter'`| Scatter plot     | Relationship between two variables  |
| `'pie'`    | Pie chart        | Proportions                         |

---

### 🔰 Example: Bar Chart

```python
df.plot(x='Day', y='Temperature', kind='bar', color='orange')
plt.title("Bar Chart - Temperature")
plt.ylabel("Temperature (°C)")
plt.show()
```

---

## 🗣️ Interview Tip – How to Explain This

> “I often use `pandas.DataFrame.plot()` for quick and clean visualizations. It’s a convenient wrapper around Matplotlib, and I can generate line plots, bar charts, and even histograms with just one line. I especially use it during EDA to visualize column trends or compare multiple variables easily.”

---

## ✅ Summary

- `df.plot()` is a shortcut to create quick visualizations from your DataFrame.
- You can use `x`, `y`, and `kind` to control what’s shown.
- Use `.show()` to display the plot.
- Great for **exploratory data analysis** and presentations.

---


