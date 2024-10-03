### Week 2: RRDtool Basics  
#### Day 8-9: RRDtool Command Line Interface

---

### 1. **Basic RRDtool Commands Overview**

RRDtool is mainly used through its **command-line interface (CLI)**. The three most essential RRDtool commands you need to understand are:

1. **rrdtool create**: This command is used to create a new RRD file (i.e., a round robin database) where your time series data will be stored.
   
2. **rrdtool update**: This is used to insert new data (time series data points) into an existing RRD.

3. **rrdtool fetch**: This command retrieves data from the RRD for analysis or graphing purposes.

Let’s go over each of these commands in detail, with practical examples.

---

### 2. **rrdtool create: Creating a New RRD Database**

The `create` command allows you to define a new RRD, including how frequently data is collected and how the data is aggregated over time.

#### **Basic Syntax**:

```bash
rrdtool create <filename> [options] [data sources] [round robin archives]
```

- `<filename>`: The name of the RRD file you are creating.
- `[options]`: Additional settings for the RRD, such as how frequently data will be collected.
- `[data sources]`: What kind of data you will store (e.g., CPU usage, network traffic).
- `[round robin archives]`: How long you want to keep the data and how it will be aggregated.

#### **Example: Creating a Simple RRD Database**:

Let’s create a database to store **CPU load** every minute, and keep data for 1 year.

```bash
rrdtool create cpu_load.rrd \
--step 60 \
DS:load:GAUGE:120:0:100 \
RRA:AVERAGE:0.5:1:525600
```

#### **Explanation**:
- **rrdtool create cpu_load.rrd**: Creates a new file called `cpu_load.rrd`.
- **--step 60**: Data will be collected every 60 seconds (1 minute).
- **DS:load:GAUGE:120:0:100**: Defines a data source (DS) for **CPU load**. 
   - `GAUGE`: The type of data source, where the value can go up and down (like CPU load or temperature).
   - `120`: This is the heartbeat, the maximum allowable time between updates (120 seconds in this case).
   - `0:100`: The acceptable range of values (minimum: 0, maximum: 100).
- **RRA:AVERAGE:0.5:1:525600**: Defines a Round Robin Archive (RRA).
   - **AVERAGE**: The data will be stored as average values.
   - **0.5**: A consolidation function that specifies the number of data points that must be present for a valid average (50%).
   - **1**: No aggregation (data is stored at its original 1-minute resolution).
   - **525600**: The total number of data points stored (60 minutes/hour * 24 hours/day * 365 days/year = 525600 minutes).

In this case, the database stores 1 year of 1-minute average CPU load data.

---

### 3. **rrdtool update: Inserting Data into the RRD**

Once you have created an RRD, you need to feed it with data. This is done using the `update` command. Each update corresponds to a timestamp and one or more data values.

#### **Basic Syntax**:

```bash
rrdtool update <filename> <timestamp>:<value1>:<value2>...
```

- `<filename>`: The name of the RRD file.
- `<timestamp>`: The time when the data was collected (either a Unix timestamp or the keyword `N` for "now").
- `<value1>`, `<value2>`: The values to insert (e.g., CPU load, network traffic, etc.).

#### **Example: Inserting Data into the RRD**:

```bash
rrdtool update cpu_load.rrd N:45
```

#### **Explanation**:
- **cpu_load.rrd**: The RRD file you are updating.
- **N**: Uses the current time as the timestamp.
- **45**: The CPU load at the current time (e.g., 45% load).

If you are inserting older data or using a specific timestamp:

```bash
rrdtool update cpu_load.rrd 1695820800:50
```

Here, `1695820800` is the Unix timestamp (seconds since January 1, 1970), and `50` is the CPU load value.

#### **Automating Updates**:
In practice, RRDtool updates are typically automated using **cron jobs** or other system monitoring tools to insert data regularly.

For example, you could set up a cron job to insert CPU load every minute by running a bash script that calls the `update` command.

---

### 4. **rrdtool fetch: Retrieving Data from the RRD**

The `fetch` command is used to retrieve data stored in the RRD for analysis, graphing, or reporting.

#### **Basic Syntax**:

```bash
rrdtool fetch <filename> <consolidation_function> --start <start_time> --end <end_time>
```

- `<filename>`: The name of the RRD file.
- `<consolidation_function>`: The aggregation method you want to use (e.g., `AVERAGE`, `MAX`, `MIN`).
- `--start <start_time>`: The start time of the data range to fetch.
- `--end <end_time>`: The end time of the data range to fetch.

#### **Example: Fetching Data**:

Let’s fetch the average CPU load over the last hour:

```bash
rrdtool fetch cpu_load.rrd AVERAGE --start -1h --end now
```

#### **Explanation**:
- **cpu_load.rrd**: The RRD file to fetch data from.
- **AVERAGE**: The aggregation function used to consolidate data.
- **--start -1h**: Fetch data starting from 1 hour ago.
- **--end now**: Fetch data up to the current time.

This will print the time series data for CPU load over the past hour, including timestamps and average CPU load values.

#### **Example Output**:

```bash
                        load
1695820800: 4.5000000000e+01
1695820860: 4.7000000000e+01
1695820920: 4.6000000000e+01
...
```

This output shows the timestamp (in Unix time) and the corresponding CPU load values.

---

### 5. **Practical Exercises**

#### **Exercise 1: Create an RRD for Monitoring Disk Usage**

Create an RRD to monitor disk usage percentage (0 to 100%) at 5-minute intervals, keeping data for 6 months.

```bash
rrdtool create disk_usage.rrd \
--step 300 \
DS:usage:GAUGE:600:0:100 \
RRA:AVERAGE:0.5:1:52560
```

Explanation:
- Data is collected every 5 minutes (`--step 300`).
- **GAUGE** is used since disk usage can go up and down.
- The RRD stores 52560 data points (60 days of 5-minute data).

#### **Exercise 2: Update Disk Usage Data**

Insert the following disk usage values (use `N` for the current time):

```bash
rrdtool update disk_usage.rrd N:55
rrdtool update disk_usage.rrd N:57
rrdtool update disk_usage.rrd N:53
```

#### **Exercise 3: Fetch Data for the Past Hour**

Retrieve the disk usage data for the past hour:

```bash
rrdtool fetch disk_usage.rrd AVERAGE --start -1h --end now
```

---

