# Running JavaScript Outside the Browser

By default, JavaScript was designed to run inside a web browser (e.g., Chrome, Firefox) to make web pages interactive. However, with **Node.js**, JavaScript can also be executed **outside the browser** on your machine or server.

---

## **How to Run JavaScript Outside the Browser**

### **1. Install Node.js**
To execute JavaScript outside the browser, you'll need to install Node.js.

1. Go to [Node.js Official Website](https://nodejs.org/).
2. Download and install the **LTS (Long Term Support)** version for stability.
3. Verify installation:
   - Open your terminal or command prompt.
   - Run:
     ```bash
     node -v
     ```
   - This will display the installed Node.js version.

---

### **2. Create a JavaScript File**
1. Use a text editor like **VS Code** to create a file with the `.js` extension.
2. Write JavaScript code in the file. For example:
   ```javascript
   console.log("Hello, Node.js!");
   ```

---

### **3. Execute the JavaScript File**
1. Open your terminal or command prompt.
2. Navigate to the directory where your JavaScript file is saved.
3. Run the file using the `node` command:
   ```bash
   node yourFileName.js
   ```
   Example:
   ```bash
   node hello.js
   ```

   **Output:**
   ```
   Hello, Node.js!
   ```

---

## **What Happens Under the Hood?**

When you run JavaScript in Node.js:
1. **Node.js takes your JavaScript code** and executes it using the **V8 engine** (the same engine used by Google Chrome to execute JavaScript).
2. It provides **additional features** that aren't available in the browser, such as:
   - Access to the file system (e.g., read/write files).
   - Networking capabilities (e.g., create servers, handle HTTP requests).
   - Built-in modules like `fs`, `http`, and `path`.

---

## **Differences Between Browser and Node.js Execution**

| **Feature**         | **Browser**                        | **Node.js**                       |
|----------------------|------------------------------------|------------------------------------|
| **Environment**      | Runs inside a browser tab/window.  | Runs in the server or terminal.   |
| **APIs**             | Access to DOM, `window` object.    | Access to `fs`, `http`, etc.      |
| **I/O Operations**   | Limited to browser sandbox.        | Full access to system resources.  |
| **Modules**          | Uses ES Modules (`import/export`). | Uses CommonJS (`require/module.exports`). |

---

## **Example: A Simple Node.js Script**

Here's a simple script that runs outside the browser to demonstrate Node.js-specific capabilities.

### **Script: Reading a File**
```javascript
const fs = require('fs'); // File system module

// Read a file named "example.txt"
fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) {
    console.error("Error reading file:", err);
    return;
  }
  console.log("File content:", data);
});
```

1. Save this script in a file, e.g., `readFile.js`.
2. Create a text file named `example.txt` in the same directory with some text.
3. Run:
   ```bash
   node readFile.js
   ```

   **Output:**
   ```
   File content: <contents of example.txt>
   ```

---

## **Conclusion**

Running JavaScript outside the browser expands its capabilities beyond web pages, making it a versatile tool for server-side programming, automating tasks, and building real-world applications. Node.js acts as the bridge to this powerful world of server-side JavaScript!
