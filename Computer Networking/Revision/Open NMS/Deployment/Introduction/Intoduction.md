### Introduction to OpenNMS Horizon

**OpenNMS Horizon** is an open-source network monitoring and management platform designed to monitor large networks. It's used by network administrators to monitor the health, performance, and availability of their networks, devices, and services. OpenNMS provides features like service availability monitoring, event management, performance data collection, and automatic device discovery, all aimed at helping network operators maintain the health of their infrastructure.

There are two versions of OpenNMS:
1. **OpenNMS Horizon** – The cutting-edge, community-driven version, updated frequently with new features and improvements.
2. **OpenNMS Meridian** – A more stable version aimed at enterprises needing long-term support and regular security updates.

### Key Features of OpenNMS Horizon

1. **Automated Network Discovery**:  
   OpenNMS can automatically discover devices and services in your network. It uses protocols like ICMP, SNMP, and other mechanisms to discover and monitor network elements, routers, switches, servers, and more.

The comparison table provided for JMX alongside other protocols is largely accurate, but let’s clarify and refine some points for better precision:

### Comparison Table: ICMP, SNMP, HTTP, SSH, WMI, JMS, JMX

| Feature                     | ICMP                                 | SNMP                                 | HTTP                                  | SSH                                   | WMI                                   | JMS                                   | JMX                                   |
|-----------------------------|--------------------------------------|--------------------------------------|---------------------------------------|---------------------------------------|---------------------------------------|---------------------------------------|---------------------------------------|
| **Purpose**                 | Network diagnostics (e.g., ping)    | Network management and monitoring     | Web services and data retrieval       | Secure remote administration            | Windows system monitoring and management | Asynchronous messaging between applications | Java application management and monitoring |
| **Protocol Type**           | Internet Layer Protocol              | Application Layer Protocol            | Application Layer Protocol             | Application Layer Protocol             | Application Layer Protocol             | Messaging Protocol                    | Application Layer Protocol             |
| **Communication Model**     | Request/Reply (typically)            | Polling and Traps                    | Request/Response                       | Request/Response                       | Event-driven, Query-based              | Publish/Subscribe or Point-to-Point   | Request/Notification                   |
| **Data Format**             | Simple message formats               | Structured data (MIBs)               | Text-based (HTML, JSON, XML)          | Text-based (command line, scripts)    | Binary and COM-based                    | Serialized Java objects, XML, JSON    | Java objects, JMX MBeans               |
| **Transport Protocol**      | Operates directly over IP            | Usually uses UDP (can use TCP)       | Usually uses TCP                       | Usually uses TCP                       | Uses DCOM over RPC                      | Typically uses TCP/IP                  | Typically uses RMI (Remote Method Invocation) |
| **Overhead**                | Low, minimal header size             | Moderate, depends on MIB size        | Higher due to HTML/JSON/XML parsing    | Moderate, depends on session overhead  | Higher due to object management          | Moderate, depends on message payload   | Moderate, depends on the MBeans       |
| **Security**                | No inherent security features         | Can use SNMPv3 for security          | Can use HTTPS for encryption           | Strong encryption and authentication    | Typically lacks encryption              | Can implement security via SSL/TLS     | Can implement security via RMI        |
| **Use Cases**               | Testing connectivity                  | Monitoring device performance         | Web service interaction                | Secure shell access to devices         | Windows performance monitoring          | Decoupling components in distributed systems | Monitoring and managing Java applications |
| **Performance Impact**      | Minimal impact                       | Can impact performance with polling   | Can be significant with large payloads | Moderate impact due to encryption      | Can be significant with many queries    | Can be significant depending on message volume | Can impact performance depending on MBeans |
| **Reliability**             | Not reliable; packets can be lost    | More reliable with retries            | Reliable with HTTP status codes        | Reliable with session management       | Reliable, but depends on DCOM setup    | Reliable with acknowledgment mechanisms | Reliable with MBean notifications      |
| **Scalability**             | Less scalable for large networks      | Highly scalable                       | Highly scalable                        | Scalable but can be limited by resources | Scalable but depends on Windows architecture | Highly scalable, especially for distributed applications | Scalable, primarily for Java applications |
| **Configuration**           | Minimal configuration                 | Requires MIBs and device setup       | Minimal configuration for endpoints    | Requires configuration of keys and access | Requires setup of WMI on target systems  | Requires configuration of message brokers | Requires setup of MBeans and connectors |
| **Common Commands**         | ping, traceroute                     | get, set, trap                        | GET, POST, PUT, DELETE                 | ssh, scp                              | Win32_* classes, queries               | send, receive, publish, subscribe      | invoke, getAttribute, setAttribute     |



### Summary of Protocols

1. **ICMP (Internet Control Message Protocol)**:
   - **Purpose**: Network diagnostics (e.g., ping).
   - **Communication**: Simple request/reply.
   - **Security**: No inherent security.
   - **Scalability**: Less scalable for large networks.

2. **SNMP (Simple Network Management Protocol)**:
   - **Purpose**: Network management and monitoring.
   - **Communication**: Polling and traps.
   - **Security**: SNMPv3 provides security features.
   - **Scalability**: Highly scalable for large networks.

3. **HTTP (Hypertext Transfer Protocol)**:
   - **Purpose**: Web services and data retrieval.
   - **Communication**: Request/response model.
   - **Security**: Can use HTTPS for encryption.
   - **Scalability**: Highly scalable.

4. **SSH (Secure Shell)**:
   - **Purpose**: Secure remote administration.
   - **Communication**: Request/response.
   - **Security**: Strong encryption and authentication.
   - **Scalability**: Scalable, limited by resources.

5. **WMI (Windows Management Instrumentation)**:
   - **Purpose**: Monitoring and managing Windows systems.
   - **Communication**: Event-driven and query-based.
   - **Security**: Typically lacks encryption.
   - **Scalability**: Depends on Windows architecture.

6. **JMS (Java Message Service)**:
   - **Purpose**: Asynchronous messaging between applications.
   - **Communication**: Publish/subscribe or point-to-point.
   - **Security**: Can implement SSL/TLS.
   - **Scalability**: Highly scalable in distributed environments.

7. **JMX (Java Management Extensions)**:
   - **Purpose**: Management and monitoring of Java applications.
   - **Communication**: Request/notification model.
   - **Security**: Can use RMI with SSL for security.
   - **Scalability**: Scalable for Java applications.

### Key Takeaways:
- Each protocol serves specific roles in network management, application monitoring, or secure communication.
- **ICMP** is focused on diagnostics, while **SNMP** and **JMX** emphasize management and monitoring.
- **HTTP** and **SSH** provide secure communication channels, and **WMI** is tailored for Windows environments.
- **JMS** supports messaging in distributed systems, making it suitable for decoupling application components. 

This summary encapsulates the essential features and use cases of each protocol, highlighting their unique strengths in network and application management contexts.

2. **Fault Management**:  
   OpenNMS can detect when devices or services are down by regularly polling them. When issues arise, it can generate alarms and notify administrators via email, SMS, or other channels. This helps reduce downtime and ensures fast issue resolution.

3. **Performance Monitoring**:  
   OpenNMS collects performance data from various devices using SNMP, JMX, HTTP, and other protocols. It can monitor CPU usage, memory consumption, bandwidth utilization, and much more. These metrics help administrators optimize and troubleshoot network performance.

4. **Service Assurance**:  
   OpenNMS monitors the availability of network services such as DNS, HTTP, FTP, and others. It can check if these services are up and running, and alert you if there is an outage.

5. **Event Management**:  
   Events generated by devices, services, or OpenNMS itself are captured and stored in a centralized system. You can define specific actions based on events, such as opening tickets, sending notifications, or executing scripts.

6. **Customizable Dashboards**:  
   The platform provides a highly customizable web interface. Users can build personalized dashboards that show the health, status, and performance of their network infrastructure in real-time.

7. **Graphing and Reporting**:  
   OpenNMS generates detailed reports and graphs based on the data collected. These reports can show network performance over time, helping administrators make data-driven decisions about network capacity and upgrades.

8. **Distributed Monitoring**:  
   OpenNMS supports distributed monitoring, allowing you to monitor remote locations without needing full instances of OpenNMS at each site. It can aggregate data from multiple sites into a central location.

9. **Scalability**:  
   OpenNMS is designed to scale from small networks with a few nodes to large enterprises with tens of thousands of devices and services to monitor.

### Core Components of OpenNMS Horizon

1. **Polling Subsystem**:  
   The polling system checks whether services are up or down. It sends out pings, HTTP requests, SNMP queries, etc., to verify service availability. If a service fails, OpenNMS raises an alarm.

2. **Event Management System**:  
   The event management system collects events from different devices and services. These events are stored in the database, allowing administrators to review network activity over time.

3. **Data Collection and Storage**:  
   OpenNMS collects performance data using SNMP, WMI, HTTP, and other methods. The collected data is stored in RRD (Round-Robin Database) files, which allow for efficient storage and retrieval of time-series data.

4. **Notifications System**:  
   Based on predefined rules, OpenNMS can send alerts through email, SMS, or other communication methods when issues occur. The notification system is highly configurable, allowing for different actions based on severity or type of issue.

5. **Provisioning System**:  
   OpenNMS supports both manual and automatic provisioning of network devices. Automatic provisioning enables the system to discover and add devices dynamically, while manual provisioning gives administrators control over what to monitor.

### Installation and Configuration

1. **System Requirements**:
   - **Operating System**: Linux-based systems (e.g., CentOS, Debian, Ubuntu)
   - **Java**: OpenNMS is a Java-based application, so a Java Runtime Environment (JRE) or Java Development Kit (JDK) needs to be installed.
   - **PostgreSQL**: OpenNMS uses PostgreSQL as its database backend. You need to install and configure PostgreSQL for OpenNMS to store its data.

2. **Installing OpenNMS**:
   - OpenNMS Horizon can be installed using package managers like `yum` (CentOS/RHEL) or `apt` (Debian/Ubuntu).
   - For example, on a **CentOS system**:
     ```bash
     sudo yum install opennms
     ```

3. **Configuring OpenNMS**:
   After installation, several configuration files control OpenNMS’ behavior. The primary ones include:
   - **`opennms.conf`**: General system configuration.
   - **`poller-configuration.xml`**: Configures how OpenNMS polls for service availability.
   - **`snmp-config.xml`**: Defines SNMP community strings and SNMP-related settings.

   Basic steps to configure OpenNMS include setting up network ranges for discovery, configuring polling and thresholds, and customizing notification rules.

4. **Starting and Stopping OpenNMS**:
   You can start OpenNMS using system commands:
   ```bash
   sudo systemctl start opennms
   ```

   To stop it:
   ```bash
   sudo systemctl stop opennms
   ```

5. **Web Interface**:
   Once OpenNMS is up and running, the web interface can be accessed by navigating to:
   ```
   http://<your_server_ip>:8980/opennms
   ```

   The web interface is where you manage and monitor your network devices, configure settings, and view performance data.

### Working with OpenNMS Horizon

1. **Discovery**:  
   Once installed, OpenNMS can automatically discover devices using ICMP and SNMP. You can also add devices manually if needed.
   
2. **Creating Monitoring Policies**:  
   Monitoring policies can be created to specify what services and devices OpenNMS should check. For example, you can create policies to monitor CPU usage on certain servers or the availability of web services.

3. **Setting Thresholds**:  
   You can set thresholds on performance data to trigger alarms. For example, if CPU usage exceeds 90% for a certain period, OpenNMS can send an alert.

4. **Configuring Notifications**:  
   Notifications can be set up to alert network administrators via email, SMS, or other methods when critical events occur. You can also specify escalation rules, ensuring that if an issue isn’t resolved in a certain timeframe, the alert is escalated to higher-level support.

5. **Viewing Alarms and Reports**:  
   Alarms are displayed in the web interface and can be acknowledged, cleared, or escalated. Reports can be generated to provide insights into network performance, including availability reports, performance trends, and SLA compliance.

### Integration with Other Tools

OpenNMS supports integration with various third-party tools and platforms:
- **Grafana**: For advanced graphing and visualization.
- **Prometheus**: To pull in Prometheus metrics for display in OpenNMS.
- **Nagios**: Integration with Nagios to extend monitoring capabilities.

### Community and Support

- **OpenNMS Community**: The OpenNMS Horizon project is community-driven, and you can find documentation, forums, and chat channels for support.
- **Documentation**: The official OpenNMS Horizon documentation provides detailed installation and configuration guides. You can refer to it for advanced setups or troubleshooting.
- **Commercial Support**: For enterprises requiring professional support, OpenNMS provides commercial support options through the Meridian version.

### Conclusion

OpenNMS Horizon is a powerful and flexible tool for network monitoring. It is ideal for IT professionals and network administrators who need to keep an eye on network health, performance, and availability. Though OpenNMS has a bit of a learning curve, it is highly customizable and can scale to monitor networks of all sizes.

By leveraging its event management, fault monitoring, and performance data collection features, OpenNMS helps ensure that your network operates smoothly and any issues are identified and resolved quickly.

---

### Basic Horizon Deployment Architecture

OpenNMS Horizon, a comprehensive network management system, follows a scalable architecture designed to monitor a wide range of network devices, services, and applications. Understanding the basic deployment architecture of OpenNMS Horizon is crucial for anyone planning to implement or maintain the system. Below is a beginner-friendly overview of the key components and architecture involved in a basic Horizon deployment.

### Key Components of Horizon Deployment Architecture

In a basic deployment of OpenNMS Horizon, several core components work together to collect data, monitor services, and present information to the user. These components include:

1. **OpenNMS Core (Daemon)**
2. **Database (PostgreSQL)**
3. **User Interface (Web UI)**
4. **Collectors and Pollers**
5. **Event Management System**
6. **Data Storage (RRD/JRB Files)**

Let’s explore these components and their roles in the Horizon architecture.

---

### 1. **OpenNMS Core (Daemon)**

The **OpenNMS core** is the primary process (daemon) that runs the application. It handles several tasks, including:

- Polling network services to check their status (up or down).
- Collecting performance data from devices.
- Managing alarms and notifications.
- Processing events generated by the network.

The core can be configured to operate at various scales, from monitoring small networks to very large ones with thousands of devices. It communicates with other components like databases, collectors, and external monitoring systems.

---

### 2. **Database (PostgreSQL)**

OpenNMS uses **PostgreSQL**, a powerful open-source relational database, to store the following critical information:

- **Events and Alarms**: Stores records of network events and any issues detected.
- **Configuration Data**: Holds information about the devices and services being monitored, their thresholds, and how they should be polled.
- **Topology Information**: Stores network topology and device discovery data.
- **Users and Roles**: Manages user accounts and permissions for the OpenNMS web interface.

PostgreSQL is a vital part of the deployment, as it ensures the persistence of network data and events for historical analysis and reporting.

---

### 3. **User Interface (Web UI)**

OpenNMS provides a **Web Interface** that allows network administrators to interact with the system. The Web UI is accessed via a browser and provides several important features:

- **Dashboards**: Customizable views of network health, performance, and alarms.
- **Reports**: Generates performance reports for services and devices.
- **Topology View**: Visual representation of the network devices and their interconnections.
- **Event and Alarm Management**: Allows users to view, acknowledge, and clear alarms.
- **Device Configuration**: Administrators can configure new devices and services to monitor via the UI.

The Web UI is a central hub for monitoring the network, visualizing data, and taking actions based on alarms or performance trends.

---

### 4. **Collectors and Pollers**

**Collectors** and **Pollers** are the backbone of OpenNMS’s data-gathering process. They interact with devices on the network to collect data and check the status of services.

#### **Pollers**:
Pollers perform checks to determine whether services (e.g., HTTP, DNS, or FTP) are up and running. These checks can be simple ICMP pings or more complex protocol-based checks (like HTTP response codes).

- **Polling** is essential for service availability monitoring, which helps detect outages or slow responses in real-time.

#### **Collectors**:
Collectors gather performance data from network devices using various protocols such as SNMP, JMX, HTTP, or custom scripts. This data includes metrics like CPU usage, memory usage, and network traffic.

- Performance data collection enables long-term trend analysis, capacity planning, and SLA (Service Level Agreement) reporting.

---

### 5. **Event Management System**

The **Event Management System** handles network events and alerts. It processes events generated by devices (e.g., SNMP traps), OpenNMS itself (e.g., service failures), or other integrated systems. Key features include:

- **Event Collection**: The system collects events from network devices (e.g., SNMP traps, syslog messages) or custom applications.
- **Alarms**: If an event indicates an issue, an alarm is generated, which can trigger notifications.
- **Correlation**: The system can correlate events, grouping related alarms into a single event to reduce noise and focus on the root cause of a problem.

The Event Management System is essential for identifying issues in real-time and taking action (like sending notifications or opening a trouble ticket).

---

### 6. **Data Storage (RRD/JRB Files)**

OpenNMS stores time-series performance data in **RRD** (Round-Robin Database) or **JRB** files. These are specialized file formats optimized for storing and retrieving historical performance data.

- **RRD/JRB Files** store network performance metrics like bandwidth usage, CPU load, memory usage, etc.
- They allow for efficient storage and quick retrieval, even when dealing with large amounts of historical data.

This data is used for generating graphs, reports, and alerts when performance thresholds are exceeded.

---

### Basic Horizon Deployment Setup

Now that we understand the key components, let’s discuss the flow of data and interactions in a basic Horizon deployment.

#### 1. **Network Discovery**:
- OpenNMS can automatically discover devices on your network using protocols like **ICMP** and **SNMP**.
- It identifies devices like routers, switches, servers, and the services running on them.

#### 2. **Polling and Data Collection**:
- Pollers regularly check the status of services (like HTTP, DNS, etc.).
- Collectors gather performance metrics from devices, such as bandwidth usage, CPU load, and memory usage.

#### 3. **Event Processing**:
- Events generated by devices (like SNMP traps or syslog messages) are collected and analyzed.
- Based on the events, OpenNMS creates alarms if necessary (e.g., a device is down or a service is failing).

#### 4. **Storage and Analysis**:
- Collected data is stored in PostgreSQL (for events/alarms) and RRD/JRB files (for performance data).
- Administrators can view this data through graphs, reports, and dashboards.

#### 5. **Notification and Alerting**:
- Based on predefined rules, OpenNMS sends notifications (via email, SMS, or other methods) when critical events occur.
- You can set up **escalation rules**, where unresolved issues are sent to higher-level administrators or teams.

---

### Deployment Models

There are several deployment models for OpenNMS Horizon, depending on the size and complexity of your network:

1. **Standalone Deployment**:
   - Suitable for small to medium-sized networks.
   - All components (OpenNMS core, PostgreSQL database, RRD/JRB files) are installed on a single server.
   - This is the most straightforward and basic deployment model.

2. **Distributed Deployment**:
   - For larger or geographically distributed networks, you can deploy collectors in remote locations (called Minions or Pollers).
   - These remote collectors gather data and send it back to a central OpenNMS instance for processing.
   - This model reduces the load on the central server and allows for better scalability.

3. **High Availability (HA) Deployment**:
   - For critical environments, you can deploy OpenNMS in an **HA setup**, where multiple instances work together to provide redundancy.
   - If one instance goes down, another takes over, ensuring continuous monitoring.

---

### Network Security Considerations

When deploying OpenNMS, network security is critical. Here are some security practices to follow:

1. **Secure Web UI**:  
   Ensure the Web UI is protected by using HTTPS and strong authentication mechanisms. You can configure SSL certificates to secure communication between users and the OpenNMS web interface.

2. **Firewall Rules**:  
   Only allow access to the OpenNMS server from trusted networks. Use firewalls to block unauthorized traffic to critical ports like PostgreSQL, SNMP, and the Web UI.

3. **Role-Based Access Control (RBAC)**:  
   Use OpenNMS’s built-in user and role management features to restrict access. Define roles for users based on their responsibilities (e.g., monitoring-only, admin access).

4. **Network Isolation**:  
   Consider placing the OpenNMS server in a separate management network that is isolated from regular user traffic. This prevents interference with network monitoring.

---

### Conclusion

A basic deployment of OpenNMS Horizon consists of a core server that handles polling, data collection, event management, and alerting, with a PostgreSQL database for storage and a Web UI for managing the system. It’s highly flexible, allowing for standalone, distributed, or high-availability deployments based on your network’s needs.

Understanding this architecture is essential for ensuring that your OpenNMS deployment is effective at monitoring your network’s performance, availability, and health. This scalable architecture allows OpenNMS to grow with your network, from small setups to enterprise-level monitoring solutions.

---

### OpenNMS Horizon: Comprehensive Notes on Installation and Configuration

OpenNMS Horizon is an open-source network monitoring and management platform. It helps monitor network devices, detect outages, and manage performance. Here's a breakdown of the key steps involved in installing and configuring OpenNMS Horizon:

---

### 1. **Installation and Configuration Overview**
The process of installing and configuring OpenNMS Horizon involves several steps, from ensuring DNS is properly set up to configuring PostgreSQL, installing the software, and finally setting up the core instance for monitoring.

---

### 2. **DNS Considerations**
Before installing OpenNMS, you should ensure that the DNS configuration is correct. DNS resolution is essential because OpenNMS needs to resolve hostnames for the nodes and devices you are monitoring.

#### Important DNS Points:
- Ensure that the **fully qualified domain name (FQDN)** of your OpenNMS server is resolvable both internally and externally.
- Set up **reverse DNS** if needed, as it helps OpenNMS properly identify devices.

### Why is DNS important for OpenNMS Horizon?
OpenNMS Horizon needs to communicate with many devices on your network. It's like a manager trying to keep track of all the employees in a big company. DNS helps OpenNMS find these devices quickly, just like how a company directory helps a manager find employees.

### DNS for beginners:
- Imagine you're setting up a big party (that's your network).
- OpenNMS is like the party planner who needs to contact all the guests (the devices on your network).
- DNS is like having a really good contact list that helps the party planner quickly find and contact each guest.

### What you need to do:
1. Make sure your computer (where you're installing OpenNMS) has a clear, unique name on the network. This is like making sure the party planner has a name tag so everyone knows who they are.
2. If possible, set up your computer to help with DNS lookups. This is like giving the party planner their own copy of the contact list, so they don't have to keep asking someone else for phone numbers.
---

### 3. **Quick Installation**

If you need to quickly install OpenNMS, the **"Quick Start"** method can help:
1. Install **Java** (OpenNMS requires Java 8 or 11).
2. Set up **PostgreSQL** (the recommended database for OpenNMS).
3. Install **OpenNMS Core** using package management (e.g., `yum`, `apt`, or `docker`).
4. Configure and launch the OpenNMS service.

- Think of it as setting up a pre-built desk versus building one from scratch.
- It's great for trying out OpenNMS or for smaller networks.
- However, for bigger networks (like managing a large office building instead of a small apartment), you might need a more custom setup later.

### What you need to do:
1. Decide if Quick Installation is right for you. If you're just learning or have a small network (like a home or small office), Quick Installation is perfect.
2. Follow the Quick Installation guide step-by-step. Don't worry if you don't understand everything at first.
---

### 4. **Scope**
OpenNMS Horizon is designed to scale across various sizes of networks, supporting hundreds of devices or large-scale enterprise setups.

#### Important Features:
- Fault and performance monitoring
- Auto-discovery of network devices
- Event and alert management
- Integration with existing tools

### For beginners:
- Think of OpenNMS like a superhero for your network.
- Its "scope" is like describing this superhero's powers and how many people they can protect.

### Key points:
1. OpenNMS can watch over very large networks (thousands of devices).
2. It's free and open-source, which means anyone can use it without paying.
3. It's good for all sizes of organizations, from small businesses to huge companies.
---

### 5. **Requirements**
Before installation, check the system and hardware requirements.

#### Basic Requirements:
- **Operating System**: Linux-based (CentOS, RHEL, Ubuntu, etc.)
- **CPU**: Minimum 4 CPU cores
- **RAM**: 8 GB minimum, but 16 GB recommended
- **Disk**: At least 20 GB of storage for the application, and more for PostgreSQL if you're monitoring many devices.
- **Java**: OpenJDK or Oracle JDK 8 or 11
- **PostgreSQL**: Version 11 or newer

---

### 6. **Set Up PostgreSQL**
PostgreSQL is the default database for OpenNMS, which stores configuration, event, and performance data.

#### Steps:
1. **Install PostgreSQL**: Use your system’s package manager, such as `yum` for RHEL-based systems or `apt` for Debian-based.
   ```bash
   sudo apt-get install postgresql postgresql-contrib
   ```
2. **Set up a PostgreSQL user and database** for OpenNMS:
   ```bash
   sudo -u postgres createuser -P opennms
   sudo -u postgres createdb -O opennms opennms
   ```
3. Modify PostgreSQL configuration for **remote access** (if needed) by editing `pg_hba.conf` and `postgresql.conf`.

4. Set up **initial connection settings** in OpenNMS using:
   ```bash
   /etc/opennms/opennms-datasources.xml
   ```


PostgreSQL 14 and 15 use the scram-sha-256 password authentication method by default. If you use older versions of PostgreSQL, you should change the method in postgresql.conf and in pg_hba.conf before installing the Horizon core instance

---

### 7. **Pool Size and Maximum Database Connections**
OpenNMS relies heavily on database performance, so configuring PostgreSQL’s connection pool size is important.

- **Connection pool size** should be set based on the number of simultaneous users and the scale of your network. A typical small installation may require 50–100 connections.
- Modify the **maximum allowed database connections** in PostgreSQL’s `postgresql.conf` to match the expected load.
  ```bash
  max_connections = 200
  ```

You must configure the PostgreSQL max_connections setting to at least twice the maximum pool size in Horizon.

The default maximum pool size value in Horizon is 50, but it applies to each connect in opennms-datasources.xml: opennms (the main connection used at runtime) and opennms-admin (the connection used during administrative operations, including installation). Therefore, your max_connections setting should be at least 100.

If you change the default pool size, make sure you also update the max_connections. You typically set this in PG_HOME/data/postgresql.conf, but you may also use the ALTER SYSTEM syntax. You must restart the PostgreSQL server for the changes to take effect.

You may find PGTune useful to calculate configuration parameters for PostgreSQL. As with all third-party tools, we do not endorse or guarantee it. Use it at your own discretion.

For larger environments, OpenNMS supports connection pooling to manage performance better.

---

### 8. **Install the Core Instance**
The core instance is the main component of OpenNMS Horizon.

#### Steps:
1. **Download and Install OpenNMS**: 
   - For RHEL/CentOS:
     ```bash
     sudo yum install opennms-core
     ```
   - For Ubuntu:
     ```bash
     sudo apt-get install opennms-core
     ```
2. **Start and enable the OpenNMS service**:
   ```bash
   sudo systemctl enable opennms
   sudo systemctl start opennms
   ```

---

### 9. **Set Up the Core Instance**
Once the core instance is installed, you need to configure it to suit your environment.

1. **Configure OpenNMS Settings** in the configuration files:
   - Modify `/etc/opennms/opennms.conf` for general settings.
   - Customize the `opennms-datasources.xml` for database connection details.
   
2. **Run Initial Setup**:
   OpenNMS provides an automatic setup script that can configure the database schema and apply basic settings:
   ```bash
   sudo /opt/opennms/bin/runjava -s
   sudo /opt/opennms/bin/install -dis
   ```

3. **Start OpenNMS Daemon**:
   ```bash
   sudo /opt/opennms/bin/opennms start
   ```

---

### 10. **First-Time Sign-In**
OpenNMS has a web-based interface for management and monitoring.

1. **Access the Web UI**: 
   Navigate to `http://<your-server-ip>:8980/opennms` in a web browser.
   
2. **Default Credentials**:
   - Username: `admin`
   - Password: `admin`

---

### 11. **Change Password After First Sign-In**
For security reasons, it is important to change the default password after the first login.

1. **Navigate to**: `Admin > Change Password`
2. **Enter the new password** and confirm it.

---

### 12. **Usage Statistics**
OpenNMS collects statistics about its usage to help improve the software and for network performance monitoring. You can enable or disable this feature based on your preferences.

To manage usage statistics:
1. Go to the `Admin` section of the web UI.
2. Select `Telemetry` to configure whether to send anonymous usage data to the OpenNMS team.

---

### 13. **First Monitored Node**
Once OpenNMS is set up, you'll want to start monitoring your first device (node).

1. **Discovery**: 
   - OpenNMS can automatically discover devices in your network. Go to `Admin > Provisioning Groups > Add New Provisioning Group`.
   - Alternatively, you can manually add nodes by specifying the IP addresses.

2. **Set up SNMP**: OpenNMS can gather detailed metrics using SNMP. Ensure that SNMP is enabled and properly configured on the device you want to monitor.

3. **Monitor the Node**:
   - The node will appear in the **Nodes** list.
   - You can view device performance, outages, and graphs from the web UI.

---

### 14. **Related Topics**
As you expand your use of OpenNMS, consider exploring more advanced topics:
- **Thresholds and Alerts**: Configure thresholds to trigger alerts when certain performance parameters (like CPU usage) exceed a set limit.
- **Performance Data Collection**: OpenNMS collects performance metrics over time, which can be visualized and analyzed through its built-in tools.
- **Integrations**: OpenNMS can be integrated with other systems like Grafana, Prometheus, and Elasticsearch.

---

### 15. **Next Steps**
After setting up your first node, here’s what you can do next:
- **Configure Alerts**: Set up email or SMS alerts to notify you of outages or performance degradation.
- **Expand Monitoring**: Add more devices and networks to be monitored.
- **Explore Advanced Features**: Dive deeper into performance monitoring, advanced provisioning, and service assurance.

---

By following these notes, you should have a functional OpenNMS Horizon instance monitoring your network.
