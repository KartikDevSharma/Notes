# Understanding Containerized Deployment of OpenNMS Horizon for Beginners

## 1. What is Containerization?

Imagine you're moving to a new house. Instead of packing everything loosely in a moving truck, you pack your belongings into standardized shipping containers. These containers are easy to stack, move, and manage. This is similar to how containerization works in software.

In the world of software:
- Your belongings = The OpenNMS Horizon application and all its dependencies
- The shipping container = A software container

Benefits:
- Consistency: OpenNMS will run the same way on any system that can run containers.
- Isolation: The OpenNMS container won't interfere with other software on the same computer.
- Easy deployment: You can quickly set up OpenNMS on different machines.

## 2. What is Docker?

Docker is like a company that standardizes these software "shipping containers" and provides tools to manage them. It's the most popular containerization platform.

In the context of OpenNMS:
- There's a pre-packaged "Docker container" for OpenNMS Horizon.
- This container includes OpenNMS and everything it needs to run.

## 3. What is Kubernetes?

If Docker helps you create and run individual containers, Kubernetes is like a fleet management system for many containers.

Imagine you're not just moving one house, but managing moves for an entire city:
- Kubernetes helps decide which moving trucks (computers) should carry which containers.
- It ensures there are enough containers of OpenNMS running to handle all the network monitoring tasks.
- If a truck (computer) breaks down, Kubernetes automatically moves its containers to other trucks.

For OpenNMS:
- Kubernetes can ensure OpenNMS is always available, even if some computers fail.
- It can automatically scale OpenNMS up or down based on how much network traffic you need to monitor.

## 4. What is Red Hat OpenShift?

OpenShift is like a deluxe version of Kubernetes created by Red Hat. It adds extra features that make it easier to use, especially for businesses.

For OpenNMS:
- If your organization uses OpenShift, it might be easier to deploy OpenNMS there.
- OpenShift provides additional security and management features.

## 5. What is Helm?

If Kubernetes is a fleet management system, Helm is like a standardized set of instructions for setting up specific types of cargo.

In software terms:
- Helm creates "charts" which are like recipes for deploying complex applications on Kubernetes.
- The OpenNMS Helm chart contains instructions on how to set up all the parts of OpenNMS in a Kubernetes environment.

For OpenNMS:
- The Helm chart simplifies the process of deploying OpenNMS on Kubernetes or OpenShift.
- It ensures that all the necessary components of OpenNMS are set up correctly and can communicate with each other.

## 6. Why Use Containerized Deployment for OpenNMS?

1. Scalability: Easily add more OpenNMS instances as your network grows.
2. Consistency: OpenNMS will behave the same way in development, testing, and production environments.
3. Resource Efficiency: Containers use resources more efficiently than traditional setups.
4. Easy Updates: Updating OpenNMS becomes as simple as pulling a new container image.

## 7. Basic Steps for Containerized Deployment of OpenNMS

1. Set up a Kubernetes or OpenShift cluster (this is like setting up your fleet of moving trucks).
2. Install Helm (this is like hiring a master coordinator for your move).
3. Use Helm to install the OpenNMS chart (this is like giving your coordinator the specific instructions for moving OpenNMS).
4. Configure OpenNMS through Kubernetes (this is like arranging your furniture in the new house).

Remember, containerized deployment is an advanced topic. If you're new to networking and OpenNMS, it's often better to start with a traditional installation on a single computer. As you grow more comfortable with OpenNMS and your monitoring needs increase, you can explore containerization as a more advanced option.

---

### OpenNMS Horizon: Comprehensive Notes on Deployment and Installation

This guide covers essential steps for deploying OpenNMS Horizon in Kubernetes or OpenShift environments, focusing on the prerequisites, external dependencies, and installation processes.

---

### 1. **Before You Begin**

Before you start deploying OpenNMS Horizon, it's important to understand a few key points:

1. **Environment Preparation**: Ensure your environment (Kubernetes or OpenShift) is ready for OpenNMS Horizon deployment. This includes having access to the necessary infrastructure, storage, and external dependencies.

2. **OpenNMS Deployment on Kubernetes/OpenShift**: OpenNMS can be deployed as containers on Kubernetes or OpenShift, which offers benefits like scalability, resilience, and ease of updates. The deployment is done using Helm charts or custom resources for easy management.

3. **Monitoring and Configuration**: OpenNMS will need to be properly configured to monitor the services and devices on your network. Ensure you understand basic networking concepts and monitoring protocols like SNMP and ICMP.

---

### 2. **Requirements**

#### a. **System Requirements**

Before deploying OpenNMS Horizon, ensure your system meets these basic requirements:

- **Cluster Requirements**:
  - A working **Kubernetes** or **OpenShift** cluster. Kubernetes version 1.19+ is recommended.
  - OpenShift version 4.x or higher for OpenShift-specific deployments.

- **Resource Requirements**:
  - **CPU**: 4 cores (minimum), but 8 cores are recommended for larger environments.
  - **Memory**: Minimum 8 GB of RAM, 16 GB is preferred for smooth operation.
  - **Storage**: Minimum 50 GB of available disk space (Persistent Volumes are required for database and data storage).
  - **Networking**: Ensure that the nodes in your cluster can communicate internally and with external networks.

- **Database**: 
  - OpenNMS Horizon requires a PostgreSQL database (version 11 or higher).
  
- **Persistent Storage**: 
  - Persistent storage is necessary for databases and collected performance data. Ensure your Kubernetes/OpenShift cluster has persistent volume support (e.g., NFS, Ceph, or AWS EBS).

---

### 3. **External Dependencies**

Several external dependencies need to be set up and configured for OpenNMS Horizon to function correctly in a containerized environment.

#### a. **PostgreSQL Database**
OpenNMS Horizon uses PostgreSQL as its backend database. When deploying on Kubernetes or OpenShift, the database can be set up as:
- A managed service, like **Amazon RDS** or **Google Cloud SQL**.
- A containerized instance deployed in the same cluster.
  
The PostgreSQL database should be pre-configured and accessible from the OpenNMS instance with appropriate credentials.

#### b. **Java Runtime**
OpenNMS Horizon requires Java to run. Typically, this dependency is handled by the container image, but you should ensure the correct Java version is specified in the container (Java 8 or 11).

#### c. **Helm**
Helm is a package manager for Kubernetes. OpenNMS Helm charts simplify the deployment and configuration process on Kubernetes. Make sure **Helm** is installed and configured to manage the Kubernetes resources.

- To install Helm:
  ```bash
  curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
  ```

#### d. **Ingress Controller**
To expose OpenNMS services outside of the cluster, you will need an Ingress controller, which allows external traffic to reach your OpenNMS deployment. Popular ingress controllers include **Nginx** and **Traefik**.

#### e. **Persistent Volume Claims (PVCs)**
You will need to configure Persistent Volume Claims (PVCs) to store data permanently. This is necessary for both PostgreSQL and OpenNMS to store logs, performance data, and configurations.

---

### 4. **Deployment on Kubernetes**

OpenNMS Horizon can be deployed on a Kubernetes cluster using Helm charts. Below is a beginner-friendly step-by-step guide for deploying OpenNMS on Kubernetes.

#### a. **Step 1: Prepare Kubernetes Cluster**
- Ensure your Kubernetes cluster is operational. You can verify this by running:
  ```bash
  kubectl cluster-info
  ```
- Check if `kubectl` (Kubernetes command-line tool) is configured to interact with the cluster.

#### b. **Step 2: Install Helm**
- Make sure Helm is installed on your machine. You can install Helm as described in the external dependencies section.

#### c. **Step 3: Add OpenNMS Helm Chart Repository**
- Add the OpenNMS Helm chart repository to your Helm installation:
  ```bash
  helm repo add opennms https://opennms.github.io/helm-charts
  helm repo update
  ```

#### d. **Step 4: Configure PostgreSQL**
You can either use a managed PostgreSQL database or deploy PostgreSQL within Kubernetes as a separate Helm chart:
- Example using the **Bitnami PostgreSQL Helm chart**:
  ```bash
  helm install my-postgresql bitnami/postgresql
  ```

Once PostgreSQL is set up, make a note of the connection details (hostname, port, username, password).

#### e. **Step 5: Install OpenNMS Horizon**
Now that the cluster is ready and the external dependencies are configured, install OpenNMS Horizon using Helm:
- Create a configuration file (`values.yaml`) to override the default settings. Specify things like database connection, persistent volumes, and resources.
- Install OpenNMS with:
  ```bash
  helm install opennms opennms/opennms -f values.yaml
  ```

#### f. **Step 6: Configure Ingress for External Access**
To make OpenNMS accessible from outside the Kubernetes cluster, set up an Ingress resource.
- Example of an Nginx Ingress:
  ```yaml
  apiVersion: networking.k8s.io/v1
  kind: Ingress
  metadata:
    name: opennms-ingress
  spec:
    rules:
    - host: opennms.example.com
      http:
        paths:
        - path: /
          pathType: Prefix
          backend:
            service:
              name: opennms
              port:
                number: 8980
  ```

---

### 5. **Installation on OpenShift**

OpenShift is a Kubernetes-based platform with added features for enterprise deployment. OpenNMS Horizon can also be installed on OpenShift using similar steps, but with some OpenShift-specific considerations.

#### a. **Step 1: Prepare OpenShift Cluster**
- Ensure you have access to an OpenShift 4.x or higher cluster.
- Use the `oc` command-line tool (OpenShift’s equivalent to `kubectl`) to interact with the OpenShift cluster.

#### b. **Step 2: Setup OpenShift Security Context Constraints (SCC)**
In OpenShift, security is stricter, and you may need to grant additional privileges to the OpenNMS pods:
1. Create a new **Security Context Constraint (SCC)** for OpenNMS that allows the necessary permissions for persistent storage access and network capabilities.
2. Grant the SCC to the OpenNMS service account:
   ```bash
   oc adm policy add-scc-to-user anyuid -z default
   ```

#### c. **Step 3: Install Helm on OpenShift**
Just like Kubernetes, Helm can be used to install OpenNMS on OpenShift. Ensure Helm is installed and configured to work with your OpenShift cluster.

#### d. **Step 4: Deploy OpenNMS Horizon**
1. Add the OpenNMS Helm chart repository and update it:
   ```bash
   helm repo add opennms https://opennms.github.io/helm-charts
   helm repo update
   ```

2. Install OpenNMS Horizon using the same process as in Kubernetes:
   ```bash
   helm install opennms opennms/opennms -f values.yaml
   ```

3. Set up any additional OpenShift-specific configurations for **networking**, **ingress**, and **security**.

#### e. **Step 5: Expose OpenNMS on OpenShift**
In OpenShift, you may need to use an **OpenShift Route** instead of Kubernetes Ingress to expose OpenNMS to external traffic.

- Example of a Route configuration:
  ```yaml
  apiVersion: route.openshift.io/v1
  kind: Route
  metadata:
    name: opennms-route
  spec:
    to:
      kind: Service
      name: opennms
    port:
      targetPort: 8980
    tls:
      termination: edge
  ```

This will expose OpenNMS Horizon to the external network, making it accessible via a browser.

---

By following these steps, you should be able to deploy OpenNMS Horizon on both Kubernetes and OpenShift environments, with all the necessary dependencies and configurations in place.
