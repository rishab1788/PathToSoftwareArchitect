
# 🚀 System Deployment at Scale

Deploying large-scale systems involves various components that need to work together seamlessly. It encompasses:

- **Application Deployment**
- **Infrastructure Deployment**
- **Operations**

Each of these areas has its unique challenges and solutions, especially when moving from monolithic to microservices-based architectures.

---

## 📦 Application Deployment Challenges

In smaller monolithic applications, deployments are straightforward. However, large-scale systems introduce **replication** and **microservices**, which create additional complexity.

- **Monolith**: Easy to deploy but difficult to scale as everything is packaged into a single artifact.
- **Microservices**: Requires careful orchestration of individual services, versioning, and dependencies.

**Challenges**:
- Managing many replicas and instances.
- Coordinating dependencies between services.
- Handling errors and rollbacks efficiently.
  
---

## 🛠 Infrastructure Deployment

Infrastructure deployment involves setting up the compute and network resources necessary for running applications.

### Components:
1. **Compute**:
   - CPU, RAM, Disks
2. **Network**:
   - Routing, Domains, Datacenters
   - Internet access, secure firewalls, and certificates
3. **Load Balancers**:
   - High-Level Balancers (HLB), Software Load Balancers (SLB)
4. **DNS & Discovery Services**
5. **Storage**:
   - Content storage, VM/container images, database backups
6. **Mail Servers**
7. **CDN** (Content Delivery Networks)

### Environments:
- **Development**, **Testing**, **Staging**, and **Production**

---

## ⚙️ Operations Workflow

Operations teams handle the deployment and maintenance of applications in a live environment. The typical workflow looks like this:

1. **Developers** create images of the application.
2. **Deployment teams** use these images to deploy across various environments (e.g., Dev, Test, Staging, Prod).
3. **Operations** teams ensure applications are running smoothly post-deployment.

---

## 🌐 Modern Deployment Solutions

- **Application Deployment**: Moving toward containers like **Docker** 🐳.
- **Infrastructure Deployment**: Shift to the **Cloud** ☁️, e.g., AWS, GCP.
- **Operations**: Managed via **Kubernetes** for container orchestration.
- **Automation**: DevOps tools like **Vagrant**, **Ansible**, and **Chef** streamline the process.

---

## 💻 Application Deployment Process

**Deploying a Web Application** involves multiple steps:
1. **Install JVM** 🖥️ (Java Virtual Machine)
2. **Install Web Container**: Jetty, Tomcat, etc.
3. **Deploy the Web App** by copying the `.war` file to the server.

**Challenges**:
- Error-prone.
- Time-consuming.
- Repetitive tasks.

**Automation** can streamline these processes:
- Provision a machine with the required OS.
- Use automation tools like **Chef** and **Ansible** to manage configuration.

---

## 🏗 Infrastructure Deployment 

Infrastructure deployment requires provisioning the right resources, including:

1. **Compute Infrastructure**:
   - Physical/virtual machines.
   - Network setup (firewalls, routing).
2. **Virtualization**:
   - Hypervisors like **ESXI** and **VMware Workstation**.
   - Virtual machines provide isolation between applications.
  
---

## 🐳 Deployment with Containers

**Containers** provide several advantages over traditional VMs:
1. **Lightweight** and can be easily copied across machines.
2. **Fast boot times** as the OS doesn't need to restart.
3. **Smaller disk space** footprint.

### Docker Example:
\`\`\`Dockerfile
FROM ubuntu

RUN apt-get install -y openjdk-11-jdk
RUN apt-get install -y jetty9

COPY ./image/war/WebApp.war /usr/war
EXPOSE 8000 8080

CMD ["usr/bin/java", "-jar", "/usr/share/jetty/start.jar"]
\`\`\`
With Docker, once the image is built, it can be deployed in any environment.

---

## ☁️ Infrastructure Deployment on the Cloud

Cloud providers, such as AWS and GCP, offer fully managed services, enabling rapid and scalable infrastructure deployment. 

### Key Features:
- **Compute VM on demand** with global availability.
- **Serverless compute** (e.g., AWS Lambda) for functions without managing servers.
- **Elastic Beanstalk** for PaaS (Platform-as-a-Service).
- **Virtual Networks** can be easily created and managed.

### Managed Services:
- **Load Balancers**: Internal, external.
- **Databases**: Managed database services (RDS, Cloud SQL).

Cloud enables the creation of environments (Dev, Staging, Prod) at scale within minutes.

---

## 🛠 Automation Tools

**Infrastructure Automation** involves using tools that provision and configure machines automatically.

1. **Vagrant**: Simplifies the creation of reproducible environments.
2. **Ansible** & **Chef**: Provide declarative infrastructure management and provisioning.

Both provide **idempotency** – ensuring that the same configuration can be applied repeatedly without changes, reducing errors.

---

# 🚢 Deployment with Kubernetes

Kubernetes (K8s) simplifies the deployment and management of containerized applications, making it possible to handle tasks like starting, stopping, and scaling containers seamlessly. Below are some of the key components and benefits of deploying applications using Kubernetes.

---

## ⚙️ Core Kubernetes Operations

### Start, Stop, and Monitor Containers

- **Start Containers**: Kubernetes manages the lifecycle of your containers, ensuring they are started based on the deployment specifications.
- **Stop Containers**: K8s gracefully terminates containers when requested, either during scaling down or replacing instances.
- **Monitor Containers**: K8s constantly monitors container health, ensuring they’re running correctly.
- **Restart Crashed Containers**: If any container crashes, K8s automatically restarts it to maintain high availability and fault tolerance.

---

## 🔗 Naming & Addressing in Kubernetes

Kubernetes abstracts away the complexities of naming and IP addressing through a **Service** object. This ensures that:

- **Project Name Abstraction**: Containers or pods don't need to reference each other by IP.
- **DNS Resolution**: K8s assigns a DNS name to services, which resolves to the underlying pods' IPs. 
- This enables **automatic discovery** and **communication** between services without needing hardcoded IP addresses.

For example, a `Service` object can be assigned a name like `my-service`, which resolves to the current set of running instances (pods).

---

## 📈 Scaling to Multiple Instances

Kubernetes enables the scaling of services effortlessly:

- Multiple instances of your application can be deployed across different pods.
- Each pod can host individual components like the **Web Layer**, **Service Layer**, and **Database Layer**.

Example of a scaled system:
```
[Web3] [Service3]  [DB3]
[Web2] [Service2]  [DB2]
[Web1] [Service1]  [DB1]
```

### Autoscaling
- Kubernetes can **autoscale** services based on traffic load or resource usage (e.g., CPU or memory).
- For instance, you can scale out to **20 instances** of a NoSQL database like **Cassandra** during high-traffic times.

---

## ⚖️ Load Balancing

One of Kubernetes' powerful features is **automated load balancing**:

- Clients talk to a **single point of contact** (Service or Ingress), and Kubernetes ensures the traffic is distributed across the healthy instances.
- **Internal Load Balancing**: Kubernetes can internally route traffic to appropriate containers.
- Kubernetes creates load balancers in an automated fashion, ensuring that each request is properly distributed among the available pods.

---

## 🛡 High Availability

Kubernetes is designed to ensure **high availability**:

- **Self-Healing**: If any pod becomes **unhealthy** or crashes, Kubernetes will automatically replace it with a healthy instance.
- **Redundancy**: Multiple pods ensure that if some instances go down, others can continue to handle requests without downtime.

This ensures your deployment is resilient and can continue to operate even if some pods fail.

---

## 🔄 Kubernetes Rolling Upgrades

Kubernetes supports **rolling upgrades** for deploying new versions of an application without downtime:

- Pods with version **V2** are deployed gradually while **V1** pods are terminated.
  
Example of rolling upgrade progression:
```
V1 V1 V2 V2 V2  -->  V1 V1 V1 V2 V2  -->  V1 V1 V1 V1 V2  -->  V1 V1 V1 V1 V1
```

This approach ensures that there is **zero downtime**, as a portion of the existing application is always running while the new version is rolled out.

### Blue-Green Deployment
Another popular deployment strategy is **blue-green deployment** where two environments (blue and green) exist simultaneously:
- **Blue** is the live environment.
- **Green** is the new version.
Once the green version is fully verified, traffic is switched to it, ensuring smooth transitions with minimal risk.

---

## 🚀 Key Benefits of Kubernetes

- **Automated Scaling**: Scale your applications up or down based on demand.
- **Self-Healing**: Crashed containers are automatically restarted.
- **Service Discovery & Load Balancing**: Easily expose and balance traffic across pods.
- **Declarative Management**: Kubernetes allows you to declare the desired state of your system, and it works to maintain that state.
- **Rolling Upgrades & Canary Deployments**: Minimize risk during deployment with smooth, zero-downtime updates.
  
Kubernetes provides the backbone for reliable, scalable, and resilient deployments in modern cloud-native applications.

---



# Kubernetes Overview 🚀

## 🛠️ Key Features

### Service Naming & Discovery 🔍
* Uses **DNS** to enable service discovery.

### Container Lifecycle Management 🔄
* Manages health checks, restarts, and replacement of unhealthy containers.

### Load Balancing ⚖️
* Built-in load balancing for distributing traffic across containers.

### Automated Rollouts and Rollbacks 🌀
* Supports smooth deployments with the ability to roll back if needed.

### Automatic Bin Packing 📦
* Allows you to specify resource requirements (e.g., CPU, memory) for containers to optimize resource usage.

### Automating Storage Mounting 💾
* Mounts storage systems of choice automatically.

---

## 🏗️ Kubernetes Network and Pods

### Logical Network 🌐
* Kubernetes creates its own logical network, ensuring that each pod can communicate with others.

### Example Deployment

```
VM -> POD1 -> [[WebApp] [LoggingApp]], ipaddress11
VM -> POD2 -> [[Services] [LoggingApp]], ipaddress12
VM -> POD3 -> [[DB] [LoggingApp]], ipaddress13
```

* Each **VM** hosts one or more **Pods**, with at least one Docker container running inside.
* **Kubernetes** ensures each pod has a unique IP and is part of a logical network.

### Example Kubernetes Deployment 🚀

```plaintext
[Browser] -> Pod[WebApp] -> Pod[Services] -> Pod[DB]
               |
               | -> Pod[WebApp] (scalable)
```

---

## Kubernetes Architecture 🏗️

### Core Components:
* **Registry**: Stores container images.
* **Kubernetes Cluster**: Manages the lifecycle of containers and ensures the desired state is met.
  * **API Server**: Entry point for commands.
  * **Controller**: Ensures the system is in the desired state.
  
### Steps for Cluster Creation ⚙️
1. Allocate VMs.
2. Install **Master** and **Proxy** components.
3. Create a **Network**.

### Steps for Operation 🎛️
* Retrieve images from the registry.
* Start and manage Pods.
* Update configuration.
* Handle events and alerts.

![Kubernetes Architecture](https://github.com/user-attachments/assets/8cb19b4d-14c5-4e8f-8427-463cfad88906)

---

## 📦 Deployment Strategies with Kubernetes

### 1. Rolling Update 🔄
* **When to use**: It’s okay to run old and new versions simultaneously.
* **How it works**: The new version is rolled out incrementally while replacing old nodes.
* **Load balancing**: Adds new nodes to the pool while removing old ones.

### 2. Canary Deployment 🐦
* **How it works**: Expose a small fraction of traffic to the new version.
* **Benefit**: Confidently roll out the update with no downtime.

### 3. Recreated Deployment 💥
* **How it works**: The old version is stopped before the new one starts. 
* **Use case**: Required when the old and new versions cannot run simultaneously.
* **Impact**: Involves a downtime.

### 4. Blue-Green Deployment 🔄💚💙
* **How it works**: The entire environment is switched to a new one using a reverse proxy.
* **Benefit**: Quick rollback to the old environment if needed.
* **Trade-off**: Avoids downtime but requires extra hardware.

### 5. A/B Testing ⚖️
* **Similar to**: Canary release but tracks user behavior across two variants.
* **How it works**: User requests are split between the two versions.
* **Benefit**: Compares feature usage and behavior.
* **Implementation**: Uses feature flags, smart logic, or switches.


  
