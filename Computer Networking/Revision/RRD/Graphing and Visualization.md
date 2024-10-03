### Week 3: Graphing and Visualization
#### Day 15-17: Basic Graphing with RRDtool


---

### 1. **RRDtool Graphing Basics**

The `rrdtool graph` command is used to create graphs from the data stored in an RRD. The graphs can display trends over time for metrics like CPU load, memory usage, network traffic, etc. This command offers many customization options, including specifying colors, labels, titles, and various types of plots.

#### **Graph Command Syntax**:
```bash
rrdtool graph <output.png> [options]
```

- **output.png**: The name of the image file that the graph will be saved as (e.g., `graph.png`).
- **options**: There are numerous options for defining data sources, graph styles, colors, titles, etc.

#### **Example**:
```bash
rrdtool graph cpu_graph.png --start -1d --end now --title "CPU Load" \
DEF:cpuload=system_stats.rrd:cpu_load:AVERAGE \
LINE1:cpuload#00FF00:"CPU Load"
```

- **`DEF:`**: Defines a data source from the RRD (in this case, the `cpu_load` data source). You specify the RRD file, the data source, and the consolidation function (`AVERAGE`, `MAX`, `MIN`, etc.).
- **`LINE1:`**: Draws a line on the graph for the `cpuload` data source. `#00FF00` specifies the line color (green), and `"CPU Load"` is the label for the line.

---

### 2. **Step-by-Step Guide to Create Simple Line Graphs**

#### **Step 1: Define the Data Source (DEF)**

The `DEF:` option allows you to define the data you want to plot from an RRD file.

```bash
DEF:cpuload=system_stats.rrd:cpu_load:AVERAGE
```
This defines `cpuload` as the **average** values of the `cpu_load` data source in the `system_stats.rrd` file. The consolidation function (`AVERAGE`) determines how the data is aggregated over time intervals.

#### **Step 2: Plot the Data (LINE)**

Once the data source is defined, you can use `LINE1`, `LINE2`, `LINE3`, etc., to draw a line on the graph. The number after `LINE` represents the thickness of the line.

```bash
LINE1:cpuload#00FF00:"CPU Load"
```

- **`cpuload`**: Refers to the previously defined data source.
- **`#00FF00`**: Specifies the line color (hexadecimal for green).
- **`"CPU Load"`**: Label that appears in the graph legend.

#### **Step 3: Set the Time Range (start/end)**

You can specify the time range for the graph using the `--start` and `--end` options.

```bash
--start -1d --end now
```

- **`--start -1d`**: Start the graph from one day ago.
- **`--end now`**: End the graph at the current time.

#### **Step 4: Add a Title**

You can give your graph a title using the `--title` option.

```bash
--title "CPU Load"
```

---

### 3. **Adding Labels and Customizing Graphs**

Once you understand the basics, you can experiment with customizing your graphs. You can add labels, adjust the axis, and play with colors to make the graph more readable and informative.

#### **Customizing Line Colors and Labels**

You can define multiple lines, each with different colors and labels. For instance, if you're plotting both CPU load and memory usage on the same graph:

```bash
rrdtool graph system_stats.png --start -1d --end now --title "System Stats" \
DEF:cpuload=system_stats.rrd:cpu_load:AVERAGE \
DEF:memusage=system_stats.rrd:memory_usage:AVERAGE \
LINE1:cpuload#00FF00:"CPU Load" \
LINE2:memusage#0000FF:"Memory Usage"
```

This creates a graph with:
- A green line for CPU load (`LINE1:cpuload#00FF00`).
- A blue line for memory usage (`LINE2:memusage#0000FF`).

#### **Adjusting Axis Labels**

You can add custom labels to the X and Y axes using the `--vertical-label` and `--x-grid` options.

```bash
--vertical-label "Load/Usage (%)"
```

This adds a vertical label to the Y-axis (representing the percentage of CPU load or memory usage).

#### **Adding a Legend**

You can use the `COMMENT` option to add custom text or legend to your graph.

```bash
COMMENT:"\n"
COMMENT:"CPU Load (green) and Memory Usage (blue)\n"
```

This adds a description below the graph.

---

### 4. **Experimenting with More Graphing Options**

Here are additional customization options to enhance your graphs:

#### **Area Graphs**

Instead of a line, you can fill the area under the line using the `AREA` option. This makes it easier to visualize the cumulative or total values over time.

```bash
rrdtool graph system_stats_area.png --start -1d --end now --title "System Stats Area Graph" \
DEF:cpuload=system_stats.rrd:cpu_load:AVERAGE \
AREA:cpuload#00FF00:"CPU Load" \
LINE1:cpuload#006600
```

- **`AREA:cpuload#00FF00`**: Fills the area under the `cpu_load` curve with green.
- **`LINE1:cpuload#006600`**: Adds a darker green line on top of the area for better visibility.

#### **Stacking Values**

You can stack multiple areas on top of each other using the `STACK` option. This is useful when plotting metrics that contribute to a total, such as different types of network traffic.

```bash
rrdtool graph network_stats.png --start -1d --end now --title "Network Traffic" \
DEF:incoming=network_traffic.rrd:incoming:AVERAGE \
DEF:outgoing=network_traffic.rrd:outgoing:AVERAGE \
AREA:incoming#00FF00:"Incoming Traffic" \
STACK:outgoing#0000FF:"Outgoing Traffic"
```

- The `STACK` option stacks the `outgoing` traffic area on top of the `incoming` traffic.

---

### 5. **Exercises to Practice**

To solidify your understanding, here are a few exercises to practice:

#### **Exercise 1: Create a Line Graph**
- Use the data in your existing RRD (e.g., CPU load and memory usage) and create a basic line graph showing these metrics over the past day.
- Experiment with colors, line thickness, and labels.

#### **Exercise 2: Create an Area Graph**
- Create an area graph for one of your data sources (e.g., CPU load).
- Use a darker color for the line on top of the area to improve readability.

#### **Exercise 3: Add a Stacked Graph**
- If you have multiple data sources in your RRD (e.g., incoming and outgoing network traffic), create a stacked graph showing both values.
- Stack the outgoing traffic on top of the incoming traffic.

#### **Exercise 4: Customize with Labels and Titles**
- Add a title, vertical axis label, and custom legend to your graph.
- Try to make your graph as informative and clear as possible.

---

### Summary

- Understand the basic syntax of the `rrdtool graph` command.
- Be able to create simple line graphs using the data in your RRDs.
- Know how to customize graphs with colors, labels, titles, and legends.
- Experiment with different types of graphs, such as area and stacked graphs, to better visualize your data.

