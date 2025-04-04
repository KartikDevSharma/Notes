
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

