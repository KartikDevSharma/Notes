### Day 22-23: Threshold and Aberrant Behavior Detection in RRDtool

---

### 1. **Thresholds in RRDtool**

A **threshold** is a predefined limit for a metric, beyond which you consider the behavior of the system to be problematic. By visualizing thresholds on a graph, you can quickly spot when a metric exceeds an acceptable range.

#### **How to Set Up a Threshold in RRDtool?**

You can visualize thresholds on your RRDtool graphs using horizontal lines, which help identify when a metric goes beyond the normal operating parameters. Typically, thresholds are used to alert about high CPU usage, memory limits, network traffic, etc.

##### **Example: Threshold for CPU Usage**
In this example, we set a **threshold** at 80% CPU usage, which is considered critical.

```bash
rrdtool graph cpu_usage_threshold.png --start -1d --title "CPU Usage with Threshold" \
DEF:cpuload=system_stats.rrd:cpu_load:AVERAGE \
LINE1:cpuload#0000FF:"CPU Load" \
HRULE:80#FF0000:"CPU Critical Threshold"
```

- **`HRULE:80#FF0000`**: Draws a red horizontal line at 80 to indicate the CPU threshold. The color **red** visually highlights critical levels.
- **Purpose**: This helps you quickly spot when CPU load exceeds the critical threshold, making it clear when intervention is necessary.

#### **Multiple Thresholds**
You can also define multiple thresholds to differentiate between **warning** and **critical** states.

##### **Example: Warning and Critical Thresholds**
```bash
rrdtool graph cpu_usage_multi_thresholds.png --start -1d --title "CPU Usage with Warning and Critical Thresholds" \
DEF:cpuload=system_stats.rrd:cpu_load:AVERAGE \
LINE1:cpuload#0000FF:"CPU Load" \
HRULE:60#FFFF00:"CPU Warning Threshold" \
HRULE:80#FF0000:"CPU Critical Threshold"
```

- **Yellow Line (`HRULE:60#FFFF00`)**: Indicates a warning threshold at 60%.
- **Red Line (`HRULE:80#FF0000`)**: Marks a critical threshold at 80%.
- **Purpose**: These multiple thresholds enable you to differentiate between moderate performance concerns (warning) and critical system overload.

---

### 2. **Aberrant Behavior Detection**

**Aberrant behavior detection** involves identifying data patterns that deviate significantly from normal behavior, which may indicate system faults, performance degradation, or potential failures.

#### **What is Aberrant Behavior?**

Aberrant behavior is when a system metric (like CPU load or network traffic) behaves unexpectedly or unusually. RRDtool provides tools to help detect these anomalies, primarily through statistical methods like **Holt-Winters forecasting**.

### **Holt-Winters Aberrant Behavior Detection**

Holt-Winters is a statistical forecasting method that can be applied to time series data to predict normal values and detect deviations. It creates a forecast and alerts you when the actual data deviates significantly from the expected range.

##### **Example: Setting Up Holt-Winters Detection**
You can use Holt-Winters for metrics that have regular seasonal patterns, such as daily CPU usage spikes during peak working hours.

1. **Enable Holt-Winters in Your RRD Creation**
   When creating your RRD database, you need to enable **Holt-Winters**:

   ```bash
   rrdtool create cpu_load.rrd --step 300 \
   DS:cpu_load:GAUGE:600:0:100 \
   RRA:AVERAGE:0.5:1:600 \
   RRA:HWPREDICT:600:0.1:0.0035:288
   ```

   - **`RRA:HWPREDICT:600`**: This sets up a **Holt-Winters prediction** archive, which stores predictions based on past data.
   - **Purpose**: Holt-Winters prediction helps RRDtool forecast what CPU load should be based on historical patterns.

2. **Detecting Aberrant Behavior**
   Once you’ve enabled Holt-Winters, you can use it to detect anomalies. You can visualize the prediction along with the actual data to see where the anomalies occur.

   ```bash
   rrdtool graph cpu_aberrant_behavior.png --start -1d --title "CPU Load with Holt-Winters Prediction" \
   DEF:cpuload=cpu_load.rrd:cpu_load:AVERAGE \
   DEF:forecast=cpu_load.rrd:cpu_load:HWPREDICT \
   LINE1:cpuload#0000FF:"Actual CPU Load" \
   LINE2:forecast#00FF00:"Forecast CPU Load" \
   ```

   - **Purpose**: The **green forecast line** represents the expected CPU load based on historical data, and the **blue line** represents actual data. Deviations from the forecast suggest aberrant behavior.

3. **Flagging Anomalies**
   RRDtool automatically flags when the actual data deviates significantly from the forecasted data.

---

### 3. **Creating Alerts Based on RRDtool Data**

Alerts notify you when certain conditions (e.g., thresholds or aberrant behavior) are met. RRDtool itself doesn't send alerts directly, but you can combine it with scripts or external tools to trigger alerts when thresholds are crossed.

#### **Creating a Simple Alert Using a Script**

You can create a basic script that checks your RRDtool data and triggers alerts when the values exceed certain thresholds.

##### **Example: Bash Script for CPU Alert**
Here’s a script that checks the current CPU load from your RRD database and sends an alert if it exceeds a critical threshold:

```bash
#!/bin/bash

# Define the RRD database and threshold
RRD_PATH="/path/to/cpu_load.rrd"
THRESHOLD=80

# Fetch the last value from the RRD
LAST_VALUE=$(rrdtool fetch $RRD_PATH LAST | tail -n 1 | awk '{print $2}')

# Check if the last value exceeds the threshold
if (( $(echo "$LAST_VALUE > $THRESHOLD" | bc -l) )); then
    echo "ALERT: CPU load is critical: $LAST_VALUE%"
    # Send an alert (you can use email, SMS, etc.)
fi
```

- **Explanation**:
  - This script fetches the **last CPU load value** and checks whether it exceeds the critical threshold (80% in this case).
  - If the threshold is exceeded, it prints an alert message. You can expand this script to send an email or an SMS using additional tools like **sendmail**, **curl**, or any messaging API.

#### **Using Monitoring Tools**

To automate alerts, you can use monitoring tools like **Nagios**, **Zabbix**, or **Prometheus** that work well with RRDtool. These tools integrate with RRDtool data to track metrics and send alerts when thresholds are exceeded or when aberrant behavior is detected.

---

### 4. **Exercises to Practice**

#### **Exercise 1: Create a Threshold Graph**
- Create a graph showing CPU usage with both a **warning** (60%) and a **critical** (80%) threshold. Use different colors for each threshold line.

#### **Exercise 2: Set Up Holt-Winters Aberrant Behavior Detection**
- Set up Holt-Winters aberrant behavior detection for CPU load. Create a graph that shows actual CPU load and the predicted values from the Holt-Winters forecast.

#### **Exercise 3: Write an Alert Script**
- Write a simple Bash script that reads data from your RRD and sends an alert if the CPU load exceeds 80%. Expand it by sending an email using **sendmail** or a similar tool.

---

### Summary

- Be able to set up **thresholds** in RRDtool graphs, visualizing warning and critical levels.
- Understand the principles of **aberrant behavior detection**, particularly using **Holt-Winters forecasting**.
- Know how to detect and visualize **anomalies** based on RRDtool data.
- Be able to create **alert systems** that trigger notifications when metrics exceed predefined thresholds.

  ---
### Day 24-25: Forecasting and Sliding Windows in RRDtool

Let's dive deeper into **forecasting** and **sliding window calculations**, which are essential for predicting future trends based on historical data. Understanding these concepts will allow you to create predictive graphs, helping you to anticipate system behavior and respond proactively to issues like system overload or performance degradation.

---

### 1. **Forecasting in RRDtool**

**Forecasting** is the process of predicting future values based on historical data patterns. In RRDtool, this is primarily done using the **Holt-Winters forecasting model**, which is well-suited for data that exhibits seasonal or cyclical behavior (e.g., network traffic peaks during the day and drops at night).

#### **How Holt-Winters Forecasting Works**

Holt-Winters forecasting uses historical data to predict future values. It accounts for:
- **Trend**: How the data changes over time.
- **Seasonality**: Recurring patterns over specific periods (e.g., daily CPU load spikes).
- **Level**: The overall average value.

RRDtool can predict the expected value of a metric and the acceptable range around it (confidence bands), which helps detect anomalies when the actual values deviate from predictions.

#### **Setting Up Holt-Winters Forecasting**

1. **Create an RRD with Holt-Winters Prediction**

You need to include Holt-Winters support when you create your RRD. This can be done using the **HWPREDICT** function.

##### **Example: Creating an RRD with Holt-Winters**
```bash
rrdtool create traffic.rrd --step 300 \
DS:incoming:GAUGE:600:0:U \
RRA:AVERAGE:0.5:1:288 \
RRA:HWPREDICT:288:0.1:0.0035:288
```

- **`HWPREDICT`**: This defines a Holt-Winters RRA that predicts future values based on the last 288 data points (approximately 1 day with 5-minute intervals).
- **`0.1:0.0035`**: These parameters control the sensitivity of the forecast model:
  - The first value (0.1) controls how quickly the forecast adapts to changes in data.
  - The second value (0.0035) is the sensitivity for detecting aberrant behavior.

2. **Creating a Predictive Graph with Forecasting**

Once you have the Holt-Winters prediction enabled, you can create graphs that include forecasted values alongside the actual data.

##### **Example: Graph with Forecasted Data**
```bash
rrdtool graph traffic_forecast.png --start -1d --title "Network Traffic with Forecast" \
DEF:actual=traffic.rrd:incoming:AVERAGE \
DEF:forecast=traffic.rrd:incoming:HWPREDICT \
LINE1:actual#0000FF:"Actual Traffic" \
LINE2:forecast#00FF00:"Predicted Traffic"
```

- **Explanation**: 
  - The **blue line** represents actual network traffic, while the **green line** represents the predicted traffic based on past data.
  - This graph helps you visualize whether the actual traffic matches the predicted values and spot anomalies when there are significant deviations.

#### **Confidence Bands**

Holt-Winters prediction also provides **upper** and **lower confidence bands**—ranges within which the actual data is expected to fall. You can visualize these bands to understand how much variation is normal.

##### **Example: Graph with Confidence Bands**
```bash
rrdtool graph traffic_with_confidence_bands.png --start -1d --title "Network Traffic with Prediction and Confidence Bands" \
DEF:actual=traffic.rrd:incoming:AVERAGE \
DEF:forecast=traffic.rrd:incoming:HWPREDICT \
DEF:upper_band=traffic.rrd:incoming:DEVPREDICT \
DEF:lower_band=traffic.rrd:incoming:FAILURES \
LINE1:actual#0000FF:"Actual Traffic" \
LINE2:forecast#00FF00:"Predicted Traffic" \
AREA:upper_band#FF9999:"Upper Confidence Band" \
LINE2:lower_band#FF0000:"Lower Confidence Band"
```

- **Upper Confidence Band**: The predicted upper limit of normal behavior.
- **Lower Confidence Band**: The predicted lower limit of normal behavior.
- **Purpose**: This graph helps you visualize when the actual traffic falls outside the expected range, indicating aberrant behavior.

---

### 2. **Sliding Window Calculations**

**Sliding window calculations** refer to analyzing data over a moving time period. Instead of analyzing a fixed historical range (like the last 24 hours), you move the window forward as time progresses, continuously analyzing the most recent data.

This technique is useful for monitoring real-time data and calculating metrics like **rolling averages** or **summations** over specific time frames.

#### **How Sliding Windows Work**

A **sliding window** defines a fixed time period over which data is aggregated. As time moves forward, the window "slides," continuously incorporating new data and discarding the oldest data.

#### **Implementing Sliding Windows in RRDtool**

1. **Sliding Window Average**

You can calculate a rolling or **sliding window average** by consolidating data over a specific period, such as the last 10 minutes or 1 hour.

##### **Example: Sliding Window for CPU Load**
```bash
rrdtool graph cpu_sliding_avg.png --start -1d --title "Sliding Average of CPU Load" \
DEF:cpuload=cpu_load.rrd:cpu_load:AVERAGE \
CDEF:sliding_avg=cpuload,300,TREND \
LINE1:sliding_avg#00FF00:"Sliding Average (5 min)"
```

- **Explanation**:
  - The **`CDEF`** (calculated data source) defines a sliding average over a 5-minute window (300 seconds).
  - The **green line** represents the average CPU load within each 5-minute window.

2. **Sliding Window Maximum/Minimum**

You can also apply a sliding window to calculate the **maximum** or **minimum** value over a given period, useful for spotting spikes or dips in the data.

##### **Example: Sliding Window for Network Traffic Max**
```bash
rrdtool graph traffic_sliding_max.png --start -1d --title "Sliding Max of Network Traffic" \
DEF:traffic=network.rrd:traffic:AVERAGE \
CDEF:sliding_max=traffic,300,MAX \
LINE1:sliding_max#FF0000:"Sliding Max (5 min)"
```

- **Explanation**:
  - This graph calculates the **maximum network traffic** within a 5-minute window and visualizes it.
  - The **red line** shows the highest traffic observed within each 5-minute sliding window.

---

### 3. **Practical Applications of Forecasting and Sliding Windows**

#### **Forecasting for Capacity Planning**
- **Example**: You can use RRDtool’s Holt-Winters prediction to forecast future CPU usage trends based on past data. This is useful for capacity planning in data centers, where you can predict when you’ll need to provision more resources (e.g., servers, storage) based on growing trends in resource usage.

#### **Sliding Windows for Real-Time Monitoring**
- **Example**: In network monitoring, you can use sliding windows to compute rolling averages of network traffic. This allows you to monitor traffic spikes in real-time and react quickly when the traffic exceeds safe operating levels.

#### **Combining Forecasting and Sliding Windows**
- You can combine sliding windows and forecasting techniques to create a more robust monitoring system. For instance, use sliding windows to calculate rolling averages and Holt-Winters to predict future behavior, allowing for real-time alerts when predictions deviate significantly from actual data.

---

### 4. **Exercises to Practice**

#### **Exercise 1: Create a Holt-Winters Forecast**
- Set up Holt-Winters prediction on an RRD containing network traffic data. Create a graph showing the actual traffic alongside the predicted traffic and confidence bands.

#### **Exercise 2: Implement a Sliding Window Average**
- Using an RRD containing CPU load data, implement a sliding window average over the last 10 minutes. Visualize the sliding window average in a graph.

#### **Exercise 3: Forecast vs. Actual**
- Compare the forecasted CPU load with actual CPU load using a Holt-Winters prediction. Use confidence bands to highlight deviations.

---

### Summary


- Understand **forecasting** techniques in RRDtool, particularly **Holt-Winters** forecasting, to predict future system behavior based on historical data.
- Be able to create graphs that display **forecasted values** and **confidence bands**.
- Know how to implement **sliding window calculations**, such as rolling averages or maxima, to analyze real-time data trends.
- Practice using these techniques in graphs to build predictive monitoring systems.


  ---
  ### Day 26-27: Integration with Web Technologies

We will learn how to integrate **RRDtool** graphs with web technologies, enabling us to create a web-based dashboard for monitoring and displaying system metrics. You'll also explore how to generate graphs dynamically for web display and integrate them with a simple web server, building the foundation for a basic monitoring solution.

---

### 1. **Generating RRDtool Graphs for Web Display**

To display **RRDtool** graphs on a web page, you can generate the graphs as images (e.g., PNG files) and embed them in HTML. RRDtool's command-line interface makes it easy to generate graphs dynamically, which can then be served via a web server.

#### **Step-by-Step Process:**

1. **Create a Graph Using RRDtool**
   First, generate a graph as a PNG image using the `rrdtool graph` command. You can automate this process by running a script periodically to update the graphs.

##### **Example: Generating a CPU Usage Graph**
```bash
rrdtool graph /var/www/html/cpu_usage.png --start -1d --title "CPU Usage (Last 24 Hours)" \
DEF:cpu_load=cpu.rrd:cpu_load:AVERAGE \
LINE1:cpu_load#0000FF:"CPU Load"
```

- **`/var/www/html/cpu_usage.png`**: The location where the graph image will be saved. This directory should be accessible by your web server (e.g., Apache or Nginx).
- **`--start -1d`**: Displays data from the last 24 hours.
- **`DEF` and `LINE1`**: Define and plot the CPU load metric on the graph.

2. **Embed the Graph in HTML**

Once you’ve generated the graph as an image, you can embed it in an HTML file.

##### **Example: HTML Code to Display Graph**
```html
<!DOCTYPE html>
<html>
<head>
    <title>System Monitoring Dashboard</title>
</head>
<body>
    <h1>System Monitoring Dashboard</h1>
    <h2>CPU Usage (Last 24 Hours)</h2>
    <img src="cpu_usage.png" alt="CPU Usage Graph">
</body>
</html>
```

- **`<img src="cpu_usage.png">`**: This embeds the generated graph in the web page. The image file is located in the same directory where the HTML file is being served from.

3. **Automate Graph Updates**
   You can set up a cron job (on Linux) to regenerate the graph periodically, ensuring that the dashboard stays up to date.

##### **Example: Cron Job to Update Graph Every 5 Minutes**
```bash
*/5 * * * * /usr/bin/rrdtool graph /var/www/html/cpu_usage.png --start -1d --title "CPU Usage (Last 24 Hours)" DEF:cpu_load=cpu.rrd:cpu_load:AVERAGE LINE1:cpu_load#0000FF:"CPU Load"
```

- **Explanation**: This cron job runs the graph generation command every 5 minutes, ensuring the graph on the dashboard is continuously updated with fresh data.

---

### 2. **Exploring Integration with Simple Web Servers**

To serve your RRDtool graphs on a web page, you'll need a web server. Here, we will discuss how to set up a simple web server like **Apache** or **Nginx** to host the dashboard.

#### **Using Apache to Serve RRDtool Graphs**

1. **Install Apache**
   If Apache is not already installed, you can install it on most Linux distributions using the following command:

   ```bash
   sudo apt-get install apache2
   ```

2. **Configure the Web Directory**
   By default, Apache serves files from `/var/www/html/`. Make sure your RRDtool graphs are saved in this directory or a subdirectory within it.

   - You can place your HTML files and images (generated by RRDtool) here for easy access:
     ```bash
     /var/www/html/dashboard.html
     /var/www/html/cpu_usage.png
     ```

3. **Access the Web Page**
   Once Apache is running, you can access the dashboard by visiting `http://localhost/dashboard.html` (or the server’s IP address).

#### **Using Python’s SimpleHTTPServer**

For quick setups or development purposes, you can use Python’s built-in **SimpleHTTPServer** to serve the graphs.

1. **Run SimpleHTTPServer**
   Navigate to the directory where your RRDtool-generated graphs and HTML files are stored, and run the following command:
   
   ```bash
   python3 -m http.server 8080
   ```

   - This starts a simple web server on port 8080. You can now access your dashboard by visiting `http://localhost:8080` in your browser.

2. **Place Your Files**
   Ensure that the HTML file and the graphs generated by RRDtool are in the same directory as where you start the server.

   ```bash
   /path/to/files/dashboard.html
   /path/to/files/cpu_usage.png
   ```

   This makes it easy to experiment with web display without needing to install a full-fledged web server.

---

### 3. **Creating a Basic Web Dashboard**

Now that you understand how to generate graphs and serve them via a web server, let's combine everything into a **basic web dashboard**.

#### **Dashboard Components:**

- **CPU Usage**
- **Memory Usage**
- **Network Traffic**
  
You can create a dashboard that dynamically displays multiple graphs, each representing a different system metric. 

##### **Example: HTML Code for a Basic Dashboard**
```html
<!DOCTYPE html>
<html>
<head>
    <title>System Monitoring Dashboard</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        h1 {
            text-align: center;
        }
        .graph {
            text-align: center;
            margin-bottom: 30px;
        }
        img {
            width: 500px;
        }
    </style>
</head>
<body>
    <h1>System Monitoring Dashboard</h1>

    <div class="graph">
        <h2>CPU Usage (Last 24 Hours)</h2>
        <img src="cpu_usage.png" alt="CPU Usage Graph">
    </div>

    <div class="graph">
        <h2>Memory Usage (Last 24 Hours)</h2>
        <img src="memory_usage.png" alt="Memory Usage Graph">
    </div>

    <div class="graph">
        <h2>Network Traffic (Last 24 Hours)</h2>
        <img src="network_traffic.png" alt="Network Traffic Graph">
    </div>
</body>
</html>
```

- **Graph Section (`<div class="graph">`)**: Each graph has its own section with a title and an embedded image.
- **Images**: These images are generated by RRDtool and saved in the same directory as the HTML file. They update periodically using a cron job.

#### **Automating the Graph Generation**
You can set up a cron job to periodically update each graph:

```bash
*/5 * * * * /usr/bin/rrdtool graph /var/www/html/cpu_usage.png --start -1d DEF:cpu_load=cpu.rrd:cpu_load:AVERAGE LINE1:cpu_load#0000FF:"CPU Load"
*/5 * * * * /usr/bin/rrdtool graph /var/www/html/memory_usage.png --start -1d DEF:mem_usage=memory.rrd:mem_usage:AVERAGE LINE1:mem_usage#FF0000:"Memory Usage"
*/5 * * * * /usr/bin/rrdtool graph /var/www/html/network_traffic.png --start -1d DEF:network=traffic.rrd:incoming:AVERAGE LINE1:network#00FF00:"Network Traffic"
```

- **Explanation**: Each cron job generates a specific graph (CPU, memory, network) every 5 minutes, ensuring the dashboard remains up-to-date.

---

### 4. **Exercises to Practice**

#### **Exercise 1: Generate a System Dashboard**
- Create an HTML dashboard with three graphs: CPU usage, memory usage, and network traffic. Generate the graphs using RRDtool and update them automatically with a cron job.

#### **Exercise 2: Experiment with Python’s SimpleHTTPServer**
- Use Python’s SimpleHTTPServer to serve your RRDtool graphs and dashboard on `localhost`. Test it by opening the dashboard in your web browser.

#### **Exercise 3: Add New Metrics**
- Extend your dashboard to include additional system metrics (e.g., disk I/O, temperature, etc.). Create corresponding RRD databases, generate graphs, and embed them in your dashboard.

---

### Summary

- Know how to **generate RRDtool graphs** for web display.
- Be able to **integrate RRDtool** with web technologies, including simple web servers like **Apache** or **Python’s SimpleHTTPServer**.
- Understand how to create a **basic web dashboard** that dynamically updates RRDtool graphs, allowing you to monitor system metrics in real-time.

---
### Day 28-29: Real-world Project – Complete Monitoring Solution

Will apply everything we’ve learned about **RRDtool** and monitoring to design and implement a real-world, end-to-end monitoring solution. The goal is to create a fully functional monitoring system that tracks key system resources (CPU, memory, disk usage) and network traffic. The solution will generate graphs that display this data and update in real time.

---

### **Step-by-Step Plan**

This plan will guide you through creating a complete monitoring solution, using **RRDtool** for data storage, graphing, and web integration.

### 1. **System Monitoring Requirements**

Before starting, let's define what resources we'll monitor:
- **CPU usage**
- **Memory usage**
- **Disk usage**
- **Network traffic**

For each resource, we will:
- Set up **RRDtool** to collect the data.
- Create **RRD databases** to store the metrics.
- Generate graphs for visualization.
- Automate the updating of data and graphs.

---

### 2. **Create RRD Databases**

You’ll need to create separate **RRD databases** for each metric you're monitoring.

#### **CPU Usage Monitoring**

1. **Create an RRD database for CPU usage**:

```bash
rrdtool create cpu.rrd \
--step 300 \
DS:cpu_load:GAUGE:600:0:100 \
RRA:AVERAGE:0.5:1:600 \
RRA:MAX:0.5:1:600
```

- **`DS:cpu_load:GAUGE`**: Defines a data source (`cpu_load`) as a GAUGE, which allows values to change freely between updates.
- **`--step 300`**: Specifies that data will be updated every 300 seconds (5 minutes).
- **RRA (Round Robin Archives)**: Stores the averages and maximums over time for trend analysis.

2. **Memory Usage Monitoring**

Similarly, create an RRD for **memory usage**:

```bash
rrdtool create memory.rrd \
--step 300 \
DS:mem_usage:GAUGE:600:0:100 \
RRA:AVERAGE:0.5:1:600 \
RRA:MAX:0.5:1:600
```

3. **Disk Usage Monitoring**

For disk usage:

```bash
rrdtool create disk.rrd \
--step 300 \
DS:disk_usage:GAUGE:600:0:100 \
RRA:AVERAGE:0.5:1:600 \
RRA:MAX:0.5:1:600
```

4. **Network Traffic Monitoring**

Network traffic typically tracks incoming and outgoing traffic separately:

```bash
rrdtool create network.rrd \
--step 300 \
DS:in_traffic:COUNTER:600:0:U \
DS:out_traffic:COUNTER:600:0:U \
RRA:AVERAGE:0.5:1:600 \
RRA:MAX:0.5:1:600
```

- **COUNTER**: Suitable for metrics like network traffic where the values continuously increase.

---

### 3. **Data Collection**

Now, you need a way to gather data from the system to populate the RRD databases. You can use shell scripts to extract system metrics and update the RRDs.

#### **CPU Usage Data Collection**

You can use the `top` or `mpstat` commands to retrieve CPU load and update the RRD database.

##### **Shell Script: Update CPU RRD**
```bash
#!/bin/bash
cpu_load=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}')  # Extract CPU usage
rrdtool update cpu.rrd N:$cpu_load
```

#### **Memory Usage Data Collection**

You can use `free` to get memory usage:

```bash
#!/bin/bash
mem_usage=$(free | grep Mem | awk '{print $3/$2 * 100.0}')  # Calculate memory usage percentage
rrdtool update memory.rrd N:$mem_usage
```

#### **Disk Usage Data Collection**

Use the `df` command to get disk usage:

```bash
#!/bin/bash
disk_usage=$(df / | grep / | awk '{print $5}' | sed 's/%//g')  # Extract disk usage percentage
rrdtool update disk.rrd N:$disk_usage
```

#### **Network Traffic Data Collection**

Use `/proc/net/dev` to extract network traffic statistics:

```bash
#!/bin/bash
in_traffic=$(cat /proc/net/dev | grep eth0 | awk '{print $2}')  # Replace eth0 with your network interface
out_traffic=$(cat /proc/net/dev | grep eth0 | awk '{print $10}')
rrdtool update network.rrd N:$in_traffic:$out_traffic
```

---

### 4. **Graph Generation**

Once data is being updated in the RRD databases, the next step is to generate graphs for each metric.

#### **CPU Usage Graph**

```bash
rrdtool graph /var/www/html/cpu_usage.png --start -1d --title "CPU Usage (Last 24 Hours)" \
DEF:cpu=cpu.rrd:cpu_load:AVERAGE \
LINE1:cpu#0000FF:"CPU Load"
```

#### **Memory Usage Graph**

```bash
rrdtool graph /var/www/html/memory_usage.png --start -1d --title "Memory Usage (Last 24 Hours)" \
DEF:mem=memory.rrd:mem_usage:AVERAGE \
LINE1:mem#FF0000:"Memory Usage"
```

#### **Disk Usage Graph**

```bash
rrdtool graph /var/www/html/disk_usage.png --start -1d --title "Disk Usage (Last 24 Hours)" \
DEF:disk=disk.rrd:disk_usage:AVERAGE \
LINE1:disk#00FF00:"Disk Usage"
```

#### **Network Traffic Graph**

```bash
rrdtool graph /var/www/html/network_traffic.png --start -1d --title "Network Traffic (Last 24 Hours)" \
DEF:in=network.rrd:in_traffic:AVERAGE \
DEF:out=network.rrd:out_traffic:AVERAGE \
LINE1:in#0000FF:"Incoming Traffic" \
LINE1:out#FF0000:"Outgoing Traffic"
```

---

### 5. **Automating the Process**

You can use cron jobs to automate the data collection and graph generation process.

#### **Update Cron Job**

Create a cron job that runs every 5 minutes to update the RRD databases:

```bash
*/5 * * * * /path/to/update_cpu.sh
*/5 * * * * /path/to/update_memory.sh
*/5 * * * * /path/to/update_disk.sh
*/5 * * * * /path/to/update_network.sh
```

#### **Graph Update Cron Job**

Similarly, automate the graph generation every 5 minutes:

```bash
*/5 * * * * rrdtool graph /var/www/html/cpu_usage.png --start -1d --title "CPU Usage (Last 24 Hours)" DEF:cpu=cpu.rrd:cpu_load:AVERAGE LINE1:cpu#0000FF:"CPU Load"
*/5 * * * * rrdtool graph /var/www/html/memory_usage.png --start -1d --title "Memory Usage (Last 24 Hours)" DEF:mem=memory.rrd:mem_usage:AVERAGE LINE1:mem#FF0000:"Memory Usage"
*/5 * * * * rrdtool graph /var/www/html/disk_usage.png --start -1d --title "Disk Usage (Last 24 Hours)" DEF:disk=disk.rrd:disk_usage:AVERAGE LINE1:disk#00FF00:"Disk Usage"
*/5 * * * * rrdtool graph /var/www/html/network_traffic.png --start -1d --title "Network Traffic (Last 24 Hours)" DEF:in=network.rrd:in_traffic:AVERAGE DEF:out=network.rrd:out_traffic:AVERAGE LINE1:in#0000FF:"Incoming Traffic" LINE1:out#FF0000:"Outgoing Traffic"
```

---

### 6. **Setting Up a Web Interface**

You can serve the graphs using a web server like Apache or Python’s SimpleHTTPServer, as covered in previous lessons.

1. **Move Graphs to the Web Directory**

Ensure your graph images are saved in `/var/www/html/` (for Apache) or the directory from which you start SimpleHTTPServer.

2. **Create a Simple HTML Dashboard**

Here’s a simple HTML template to display the graphs:

```html
<!DOCTYPE html>
<html>
<head>
    <title>System Monitoring Dashboard</title>
</head>
<body>
    <h1>System Monitoring</h1>

    <h2>CPU Usage</h2>
    <img src="cpu_usage.png" alt="CPU Usage">

    <h2>Memory Usage</h2>
    <img src="memory_usage.png" alt="Memory Usage">

    <h2>Disk Usage</h2>
    <img src="disk_usage.png" alt="Disk Usage">

    <h2>Network Traffic</h2>
    <img src="network_traffic.png" alt="Network Traffic">
</body>
</html>
```

---

### 7. **Project Summary**

At the end of Day 28-29, you will have created a full monitoring system that:
- **Collects data** for CPU, memory, disk usage, and network

 traffic.
- **Stores the data** in RRD databases.
- **Generates graphs** dynamically to visualize trends and statistics.
- **Automates updates** with cron jobs.
- **Displays the graphs** on a simple web interface using a web server.

This project mirrors real-world DevOps and network monitoring tools, preparing you to build scalable, custom monitoring solutions.

---



