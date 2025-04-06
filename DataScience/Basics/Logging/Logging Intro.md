
# 🧠 What is Logging?

**Logging** is like a smart diary your program keeps.  
It **records messages** that help you understand:

- What your code is doing
- When it’s doing it
- If anything goes wrong (like errors)
- How long tasks take

It’s way more powerful than `print()` because:
✅ You can control the **level of importance**  
✅ You can **write logs to files**  
✅ You can use it for **debugging, monitoring**, or **reporting**

---

## 🔧 Basic Logging Example

```python
import logging

logging.basicConfig(level=logging.INFO)

logging.info("This is an info message.")
logging.warning("This is a warning.")
logging.error("This is an error!")
```

### Output:

```
INFO:root:This is an info message.
WARNING:root:This is a warning.
ERROR:root:This is an error!
```

---

## 🎯 What are Logging Levels?

These are like **priorities** of messages. You can choose what gets logged:

| Level       | Purpose                            |
|-------------|-------------------------------------|
| `DEBUG`     | Detailed info, for debugging only   |
| `INFO`      | General information (e.g. start/end of task) |
| `WARNING`   | Something might be wrong            |
| `ERROR`     | Something went wrong but program runs |
| `CRITICAL`  | Big problem! Program might crash    |

---

## 📁 Logging to a File

Instead of printing everything on screen, log it into a file.

```python
import logging

logging.basicConfig(
    filename='app.log',
    filemode='w',  # 'a' to append, 'w' to overwrite
    format='%(asctime)s - %(levelname)s - %(message)s',
    level=logging.DEBUG
)

logging.debug("Debugging something...")
logging.info("Starting the program")
logging.warning("Disk almost full")
logging.error("Could not open file")
logging.critical("System crash!")
```

### Output (in `app.log` file):

```
2025-04-04 19:10:12,345 - DEBUG - Debugging something...
2025-04-04 19:10:12,346 - INFO - Starting the program
2025-04-04 19:10:12,347 - WARNING - Disk almost full
2025-04-04 19:10:12,348 - ERROR - Could not open file
2025-04-04 19:10:12,349 - CRITICAL - System crash!
```
Let's break down these two lines of code in the **logging configuration** to understand **what they do** in detail:

### 1. `format='%(asctime)s - %(levelname)s - %(message)s'`

This specifies the **overall format** of the log messages. It tells Python's `logging` module how to structure each log entry.

- **`%(asctime)s`**: This placeholder will insert the **timestamp** (date and time) when the log message was created. This is controlled by the `datefmt` parameter.
- **`%(levelname)s`**: This placeholder inserts the **log level**, such as `DEBUG`, `INFO`, `WARNING`, `ERROR`, or `CRITICAL`. This helps you understand the severity of the log message.
- **`%(message)s`**: This is where the **actual log message** you pass (e.g., `"This is an info message."`) will be inserted.

In practice, the **`format`** will look something like:

```
2025-04-04 14:35:45 - INFO - This is an info message.
```

The **`asctime`** will be formatted according to the **`datefmt`** parameter, and the **`levelname`** will show the log level (`INFO`, `DEBUG`, etc.). Finally, the **`message`** is the custom text you provide in the logging call.

### 2. `datefmt='%Y-%m-%d %H:%M:%S'`

This is where you define how the **timestamp** (i.e., `asctime`) should look in your log entries.

- **`%Y`**: This will output the **4-digit year** (e.g., `2025`).
- **`%m`**: This will output the **2-digit month** (e.g., `04` for April).
- **`%d`**: This will output the **2-digit day of the month** (e.g., `04`).
- **`%H`**: This will output the **2-digit hour** in **24-hour format** (e.g., `14` for 2 PM).
- **`%M`**: This will output the **2-digit minute** (e.g., `35`).
- **`%S`**: This will output the **2-digit second** (e.g., `45`).

So the **timestamp** will appear like this:

```
2025-04-04 14:35:45
```

### Putting It All Together

When you combine both `format` and `datefmt`, this is what happens:

- **`%(asctime)s`** will show the **current date and time**, formatted as specified by `datefmt`.
- **`%(levelname)s`** will show the **log level** (e.g., `INFO`, `ERROR`).
- **`%(message)s`** will show the **log message** you wrote.

### Example Code:

```python
import logging

# Configure logging
logging.basicConfig(
    level=logging.DEBUG,  # Set log level to DEBUG (shows all messages)
    format='%(asctime)s - %(levelname)s - %(message)s',  # Define log format
    datefmt='%Y-%m-%d %H:%M:%S'  # Define date and time format
)

# Example log messages
logging.debug("This is a debug message.")
logging.info("This is an info message.")
logging.warning("This is a warning message.")
logging.error("This is an error message.")
logging.critical("This is a critical message.")
```

### Output:

```
2025-04-04 14:35:45 - DEBUG - This is a debug message.
2025-04-04 14:35:45 - INFO - This is an info message.
2025-04-04 14:35:45 - WARNING - This is a warning message.
2025-04-04 14:35:45 - ERROR - This is an error message.
2025-04-04 14:35:45 - CRITICAL - This is a critical message.
```

### Explanation of the Output:

- **`2025-04-04 14:35:45`**: This is the **timestamp** generated by `%(asctime)s`, formatted according to `datefmt='%Y-%m-%d %H:%M:%S'`.
- **`DEBUG`, `INFO`, `WARNING`, etc.**: These are the **log levels** generated by `%(levelname)s`.
- **The text after the timestamp and log level**: This is the **log message** you pass when logging.

### Conclusion:
- `format='%(asctime)s - %(levelname)s - %(message)s'` dictates the **overall structure** of your log message.
- `datefmt='%Y-%m-%d %H:%M:%S'` specifies the **format** of the timestamp that appears in the log.


Together, they ensure that every log entry is timestamped and clearly shows the log level and message, making it easier to track and debug your application.

---

## 📌 Use Case: Logging in a Real Script

Let’s say you're processing a dataset:

```python
import logging
import pandas as pd

# Setup logging
logging.basicConfig(
    filename="processing.log",
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

def load_data(path):
    try:
        data = pd.read_csv(path)
        logging.info(f"Loaded data from {path} successfully.")
        return data
    except FileNotFoundError:
        logging.error(f"File {path} not found.")
    except Exception as e:
        logging.critical(f"Unexpected error: {e}")

# Example usage
df = load_data("data.csv")
```

🔍 Instead of crashing your program, now you’ll have a clear log of what happened.

---

## 🧰 BONUS: Add Logging to Your Own Functions

Let’s say you wrote a function to process images or do math:

```python
def divide(a, b):
    try:
        result = a / b
        logging.info(f"Divided {a} by {b} successfully.")
        return result
    except ZeroDivisionError:
        logging.error("Attempted to divide by zero!")
        return None
```

---

## 🧠 Interview Tip: What to Say

> “Instead of using print statements for debugging, I use Python’s `logging` module. It lets me control the level of detail, write logs to a file, and monitor the behavior of my script more efficiently. For example, when working with data pipelines or model training, I log every major step, like loading data, model start/stop, and error handling. I also customize the format and log level depending on whether I’m in development or production.”

---

## 🔄 Summary

✅ Use `logging` instead of `print()`  
✅ Understand logging levels (`DEBUG`, `INFO`, etc.)  
✅ Save logs to file with `basicConfig()`  
✅ Wrap risky code in `try-except` and log errors  
✅ Helps in debugging, audits, or production tracking  

---

---

Perfect, Kartik! You're now getting into more **real-world logging setups** — using **multiple loggers** is a very practical and *interview-worthy* skill, especially in **bigger projects or pipelines** (like data science, ML, APIs, etc.).

Let’s break this down in the **simplest and most memorable way**, and by the end you’ll be able to confidently say:

> *“I know how to create and manage multiple loggers, customize their outputs, and control log levels separately for different parts of my code.”*

---

# 🎯 Why Use Multiple Loggers?

When your codebase grows, you **don’t want all logs mixed together**.  
Instead, you want:

- `data_logger` for logging dataset issues  
- `model_logger` for logging training steps  
- `api_logger` for logging requests/errors  
- ...all writing to different files or with different rules

---

# 🛠️ Step-by-Step: Using Multiple Loggers in Python

Let’s build a real-world simulation:

✅ Logger for data loading  
✅ Logger for model training  
✅ Each writes to a separate log file  
✅ Different formats and levels

---

## 📁 Project Structure (Mental Map)

```plaintext
project/
│
├── main.py
├── data_utils.py   # has data_logger
└── model_utils.py  # has model_logger
```

---

## ✅ Step 1: Create Custom Loggers

### 🔹 data_utils.py

```python
import logging

# Create a logger for data tasks
data_logger = logging.getLogger("data_logger")
data_logger.setLevel(logging.INFO)

# File handler for writing logs to file
data_file = logging.FileHandler("data.log")
data_format = logging.Formatter('%(asctime)s - DATA - %(levelname)s - %(message)s')
data_file.setFormatter(data_format)

data_logger.addHandler(data_file)

def load_data():
    data_logger.info("Loading data started...")
    try:
        # Simulated loading
        x = [1, 2, 3]
        data_logger.info("Data loaded successfully.")
        return x
    except Exception as e:
        data_logger.error(f"Error loading data: {e}")
```

---

### 🔹 model_utils.py

```python
import logging

# Create a logger for model tasks
model_logger = logging.getLogger("model_logger")
model_logger.setLevel(logging.DEBUG)

# File handler for model logs
model_file = logging.FileHandler("model.log")
model_format = logging.Formatter('%(asctime)s - MODEL - %(levelname)s - %(message)s')
model_file.setFormatter(model_format)

model_logger.addHandler(model_file)

def train_model(data):
    model_logger.info("Training started...")
    try:
        for epoch in range(3):
            model_logger.debug(f"Epoch {epoch + 1} - processing data: {data}")
        model_logger.info("Model trained successfully.")
    except Exception as e:
        model_logger.critical(f"Training failed: {e}")
```

---

## ✅ Step 2: Use Both in main.py

```python
from data_utils import load_data
from model_utils import train_model

data = load_data()
train_model(data)
```

Now when you run `main.py`, you'll get two log files:

- `data.log` — only has logs related to data
- `model.log` — only has logs related to training

---

## 🧠 Summary: What's Happening?

| Concept        | What You Did                              |
|----------------|--------------------------------------------|
| Custom logger  | `logging.getLogger("name")`                |
| File handler   | `logging.FileHandler()` writes to file     |
| Formatter      | Controls log line appearance               |
| Separate files | Each logger logs to its own `.log` file    |
| Levels         | You can set different `setLevel()` for each|

---

## 🧠 Bonus Tip: Logging to Console + File at Same Time

You can add **both a `FileHandler` and `StreamHandler`**:

```python
console_handler = logging.StreamHandler()
console_handler.setFormatter(logging.Formatter('%(levelname)s: %(message)s'))

logger.addHandler(console_handler)
```

Now, logs show up in the terminal *and* save to file.

---

## 🎤 Interview Answer Template

> “In large applications, I create multiple loggers with unique names using `getLogger()`, like `data_logger`, `model_logger`, etc. Each logger can have its own level, handler (file or console), and formatter. This helps in keeping logs organized and debugging easier. For example, in one project I used separate logs for data processing, model training, and API errors, which made tracking issues much cleaner.”

---
Absolutely, Kartik! Let's walk through a **real-world logging example** in a **data science pipeline** — the kind you might actually build or work on during an internship or job.

We’ll simulate a basic workflow:

---

## 🧪 Scenario: You're Building a Data Science Pipeline

Your pipeline has the following steps:

1. Load data from a CSV file  
2. Clean the data  
3. Train a dummy model  
4. Save the trained model  

You want to **log every major step**, **handle errors**, and **track progress** in a clean and structured way.

---

## 🧱 Project Layout

Everything in a single script for simplicity:

```plaintext
pipeline.py
```

---

## 📄 Full Code with Logging (Beginner-Friendly)

```python
import logging
import pandas as pd
import pickle
from sklearn.linear_model import LinearRegression

# -------------------------------
# 🔧 Step 1: Setup the Logger
# -------------------------------
logging.basicConfig(
    filename='pipeline.log',
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

# -------------------------------
# 🧹 Step 2: Load and Clean Data
# -------------------------------
def load_data(filepath):
    logging.info(f"Trying to load data from {filepath}")
    try:
        df = pd.read_csv(filepath)
        logging.info(f"Loaded data successfully with shape {df.shape}")
        return df
    except FileNotFoundError:
        logging.error(f"File {filepath} not found.")
    except Exception as e:
        logging.critical(f"Unexpected error while loading data: {e}")

def clean_data(df):
    logging.info("Starting data cleaning...")
    try:
        df_cleaned = df.dropna()
        logging.info(f"Removed missing values. New shape: {df_cleaned.shape}")
        return df_cleaned
    except Exception as e:
        logging.error(f"Data cleaning failed: {e}")
        return df

# -------------------------------
# 🧠 Step 3: Train a Dummy Model
# -------------------------------
def train_model(df):
    logging.info("Starting model training...")
    try:
        X = df[['feature1']]  # assume one feature
        y = df['target']      # assume target column
        model = LinearRegression()
        model.fit(X, y)
        logging.info("Model training completed.")
        return model
    except Exception as e:
        logging.critical(f"Model training failed: {e}")

# -------------------------------
# 💾 Step 4: Save Model to Disk
# -------------------------------
def save_model(model, filename='model.pkl'):
    try:
        with open(filename, 'wb') as f:
            pickle.dump(model, f)
        logging.info(f"Model saved to {filename}")
    except Exception as e:
        logging.error(f"Failed to save model: {e}")

# -------------------------------
# 🚀 Step 5: Main Pipeline
# -------------------------------
def main():
    logging.info("Pipeline started.")
    
    df = load_data("data.csv")  # this file must exist
    if df is None:
        logging.critical("Stopping pipeline due to data load failure.")
        return

    df_clean = clean_data(df)
    model = train_model(df_clean)
    
    if model:
        save_model(model)
    
    logging.info("Pipeline completed.")

if __name__ == "__main__":
    main()
```

---

## 📘 What You Learn From This Example

### 🔹 Logging Real Steps
Each real step (`load`, `clean`, `train`, `save`) is logged.

### 🔹 Logging Errors Properly
If anything fails, it's **not crashing blindly** — the error is logged, and the pipeline continues or stops as needed.

### 🔹 File Logging
All logs are stored in `pipeline.log` for later review, useful for debugging or auditing.

### 🔹 Good Practices
- Using `try-except` blocks around risky operations
- Logging **start and end** of each function
- Including **data shapes** to track progress

---

## 📁 Sample Log Output

```log
2025-04-04 20:03:55,092 - INFO - Pipeline started.
2025-04-04 20:03:55,093 - INFO - Trying to load data from data.csv
2025-04-04 20:03:55,152 - INFO - Loaded data successfully with shape (1000, 2)
2025-04-04 20:03:55,153 - INFO - Starting data cleaning...
2025-04-04 20:03:55,154 - INFO - Removed missing values. New shape: (950, 2)
2025-04-04 20:03:55,156 - INFO - Starting model training...
2025-04-04 20:03:55,158 - INFO - Model training completed.
2025-04-04 20:03:55,159 - INFO - Model saved to model.pkl
2025-04-04 20:03:55,160 - INFO - Pipeline completed.
```

---

This is the kind of logging setup you can **easily use in real data science projects**, even when you scale up to:

- Jupyter notebooks
- Training loops
- APIs
- Cloud jobs (e.g. AWS Lambda, GCP, Airflow)

---


