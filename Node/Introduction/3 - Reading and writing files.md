# Reading and Writing Files in Node.js

In Node.js, file operations are handled using the built-in **`fs` (File System)** module. This module allows you to perform tasks like reading, writing, deleting, and updating files in your local file system.

---

## **Basic File Operations**

### **1. Import the `fs` Module**

To work with files, you need to require the `fs` module:

```javascript
const fs = require('fs');
```

---

### **2. Reading Files**

Node.js provides two primary methods to read files:

#### **a) Asynchronous Reading (`fs.readFile`)**
The asynchronous method reads files without blocking the event loop.

```javascript
fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error reading file:', err);
    return;
  }
  console.log('File content:', data);
});
```

- **Parameters:**
  - `'example.txt'`: The file path.
  - `'utf8'`: Encoding format (optional; ensures readable text).
  - `callback`: A function to handle the result (`err` and `data`).

#### **b) Synchronous Reading (`fs.readFileSync`)**
The synchronous method blocks execution until the file is fully read.

```javascript
try {
  const data = fs.readFileSync('example.txt', 'utf8');
  console.log('File content:', data);
} catch (err) {
  console.error('Error reading file:', err);
}
```

---

### **3. Writing Files**

You can write data to a file using these methods:

#### **a) Asynchronous Writing (`fs.writeFile`)**
Creates or overwrites a file with the specified content.

```javascript
fs.writeFile('example.txt', 'Hello, Node.js!', (err) => {
  if (err) {
    console.error('Error writing to file:', err);
    return;
  }
  console.log('File written successfully!');
});
```

#### **b) Synchronous Writing (`fs.writeFileSync`)**
Writes data to a file synchronously, blocking the event loop.

```javascript
try {
  fs.writeFileSync('example.txt', 'Hello, Node.js!');
  console.log('File written successfully!');
} catch (err) {
  console.error('Error writing to file:', err);
}
```

---

### **4. Appending to a File**

To add content to an existing file without overwriting, use the following methods:

#### **a) Asynchronous Appending (`fs.appendFile`)**
```javascript
fs.appendFile('example.txt', '\nAppended text.', (err) => {
  if (err) {
    console.error('Error appending to file:', err);
    return;
  }
  console.log('Text appended successfully!');
});
```

#### **b) Synchronous Appending (`fs.appendFileSync`)**
```javascript
try {
  fs.appendFileSync('example.txt', '\nAppended text.');
  console.log('Text appended successfully!');
} catch (err) {
  console.error('Error appending to file:', err);
}
```

---

### **5. Deleting Files**

To remove a file, use:

#### **a) Asynchronous Deletion (`fs.unlink`)**
```javascript
fs.unlink('example.txt', (err) => {
  if (err) {
    console.error('Error deleting file:', err);
    return;
  }
  console.log('File deleted successfully!');
});
```

#### **b) Synchronous Deletion (`fs.unlinkSync`)**
```javascript
try {
  fs.unlinkSync('example.txt');
  console.log('File deleted successfully!');
} catch (err) {
  console.error('Error deleting file:', err);
}
```

---

### **6. Checking if a File Exists**

Before performing operations, you might want to check if a file exists:

#### **Asynchronous Check (`fs.access`)**
```javascript
fs.access('example.txt', fs.constants.F_OK, (err) => {
  if (err) {
    console.log('File does not exist.');
  } else {
    console.log('File exists.');
  }
});
```

#### **Synchronous Check (`fs.existsSync`)**
```javascript
if (fs.existsSync('example.txt')) {
  console.log('File exists.');
} else {
  console.log('File does not exist.');
}
```

---

## **JavaScript Revision for Callbacks**

File operations often use **callbacks** to handle asynchronous tasks. Here's a quick review:

### **Example: Callback Function**
```javascript
function greet(name, callback) {
  console.log(`Hello, ${name}`);
  callback();
}

greet('Alice', () => {
  console.log('This is a callback function.');
});
```

- **Why Use Callbacks?**
  Callbacks ensure certain code runs only after an asynchronous operation is complete.

---

## **Key Differences: Asynchronous vs Synchronous**

| **Aspect**           | **Asynchronous**                  | **Synchronous**                  |
|-----------------------|------------------------------------|-----------------------------------|
| **Execution**         | Non-blocking                      | Blocking                          |
| **Performance**       | Suitable for large files/servers  | May block the event loop          |
| **Code Example**      | `fs.readFile`, `fs.writeFile`     | `fs.readFileSync`, `fs.writeFileSync` |

---

## **Practice Exercise**

1. Create a file named `notes.txt`.
2. Write "This is my first note" to the file.
3. Append "This is an appended note."
4. Read the file and display its content.
5. Delete the file.

---

