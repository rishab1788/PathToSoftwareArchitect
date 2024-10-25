Architecting Solution with platform & Frameworks
* Platforms for
    * WebApps
    * Services
    * Datastores
    * Analytics
* Platform Functionality
* Platform Architecture
    * Performance
    * Scalability
    * Reliability
* Platform Use-cases
* Platform Alternatives
* Architecting Solution
    * End-to-End
 
Refrence System 
<img width="1158" alt="image" src="https://github.com/user-attachments/assets/53bea21a-6eef-424a-b4a6-717f5aeafb3e">
build the system. functionallity of the product 

# Web Applications Overview 🌐

## Frontend Systems (DB Gets Less Load) ⚡
- **Request Load**: Every request to the frontend may or may not be sent to the database.
- **Solutions for Web Applications**:
  - **Static Content** 🖼️
    - Apache Web Server 🏗️
    - Nginx Web Server 💡
    - Cloud Storage ☁️
  - **Dynamic Content** 🔄
    - Web Server: Apache HTTPD, NodeJS 🌍
    - Java Web Container: Tomcat, Jetty, Spring Boot ☕
  - **Content Caching** 🧊
    - Nginx 🔁
  - **Content Distribution** 🌍
    - CDN (Content Delivery Network)

---

## Apache Web Server 🏗️

- **Handles Static Content** 🖼️:
  - HTML/CSS/JS files 🖥️
  - Image Files 🖼️
  - Documents 📄
  
- **Generates Dynamic Content** 🔄:
  - Supports PHP, Python, Perl 🐍
  - Fetches data from the page and generates content
  - Does not support JSP/Servlets ❌

- **Acts as Reverse Proxy (but not the best option)** 🚫
  
### Architecture (Request-Response Model) 🔄

![Apache Architecture](https://github.com/user-attachments/assets/df22375c-b41b-4e4d-a531-489a16edbd3c)

---

## Nginx Web Server 💡

- **Handles Static Content** 🖼️:
  - HTML/CSS/JS files 🖥️
  - Images 🖼️
  - Documents 📄
  
- **Generates Dynamic Content** (not the best at it) ❌

- **Acts as a Reverse Proxy (performs exceptionally well)** 🔀

### Event-Driven Architecture 🧠
- Handles **1 million connections** with a single thread.

![Nginx Architecture](https://github.com/user-attachments/assets/f82400d1-c3f3-4d74-9d9e-4d2183269936)

---

## Web Containers 🛠️

- **Tomcat/Jetty** for Servlets and Spring-based applications ⚙️
- **Application Servers**: Wildfly/JBoss 🖥️
- **Spring Boot** embeds web containers like Tomcat/Jetty 🌱

### MVC Architecture:
- **Servlets** for logic ⚙️
- **JSP** for presentation 🎨

### Spring Framework 🖥️
- **IOC/DI**: For business logic 🧠
- **MVC**: For frontend and service logic 🎨
- **JDBC Template**: For database access 💾
- **Connection Pools**: HTTP and DB connections 🔗

---

## Node.js 🚀

- **Efficient HTTP Server** powered by JavaScript engine ⚡
- Ideal for **IO-bound** tasks (DB or file operations) 🗃️
- Single-threaded architecture 🧵, handles multiple connections.

![Node.js Architecture](https://github.com/user-attachments/assets/e46e3f49-725a-42ee-a0b9-a85f00cb9a74)

---

## Cloud Solutions for Web ☁️

### Managed Services 🛠️
- **Hardened Solutions** 🔐
- **Automated Deployment** 🤖
- **Built-in Scalability & Reliability** ⚙️
- **Global Deployment** 🌍

### Cloud Storage 💾
- **Unlimited Disk Space** 📂
- **Version Control** 📑
- **Access Control** 🛡️
- **Low Latency** ⚡
- **High Availability & Reliability** 🔄
- **Static Website Creation** 🏗️

### Cloud CDN (Content Delivery Network) 🌍
- **Low Latency** for cache hits ⚡
- **Persistent Connections** for cache misses 🔁
- **Reduces Backend Load** 🧑‍💻

---

## Service Layers & Caching 🧊

- **Business Logic in Services** 🛠️
- **Web Containers**: REST and Spring-based containers ⚙️
- **Object Caching**: Memcached & Redis 🗃️
- **Async Messaging**: Redis, RabbitMQ, Kafka 📬
- **Service Mesh**: Netflix, Istio 📡

---

## Memcached 🧊

- **Key-Value Store** for fast access ⚡
- **Values**: Any size (preferred < 1MB), configurable max size 📦
- **Sub-millisecond Latency** ⚡
- **Horizontally Scalable** ↔️
- **Cache-Aside Pattern** 🛠️
  
  **Architecture**: 

  ![Memcached Architecture](https://github.com/user-attachments/assets/69a39ef3-96de-4d34-bf72-10e6a1243213)

**Biggest Drawback**: Data is lost if a node crashes or is restarted 🚨

---

## Redis Cache 🗃️

- **Key-Value & Data Structures Store** 🗂️:
  - Supports Strings, Lists, Sorted Sets, Maps, etc.
  
- **Persistent Store**:
  - Stores data on disk 💾
  - Backup & restore capabilities 📂
  
- **Data Replication**:
  - Asynchronous & synchronous options 🔁
  
- **Messaging Queue** capabilities 📬

  **Architecture**:

  ![Redis Architecture](https://github.com/user-attachments/assets/e52206c8-0c22-4dbb-b27a-80d307fcc513)

### Cloud Caching Solutions ☁️
- **AWS ElastiCache**:
  - Supports Memcached & Redis 🗄️
- **Google Memorystore**:
  - Fully managed Redis or Memcached ⚡
  
- **Features**:
  - Sub-millisecond latency ⚡
  - Scalable up to 5TB 📊
  - High availability (99.9%) 💡

---

## RabbitMQ 📬

- **Messaging Queue** for async communication between services 📨
- **Supports Multiple Patterns**:
  1. One-to-one messaging 📤
  2. One-to-many messaging 📥
  3. Pull-based messaging ↔️

### Design Goals:
- **At Least Once Delivery** 📩
- **Message Sequencing (FIFO)** ⏳
- **Interface & Consumer Decoupling** ✂️
- **Message Rate Decoupling** 🔄

### Use Cases:
- **Service Integration** 🔄
- **Message Buffer** 📦
 
# Messaging Architecture Comparison 📡

## 🐰 RabbitMQ
- **General-purpose message broker** used for managing asynchronous messaging between systems.
- **Message Lifecycle**: Messages are deleted once acknowledged, ensuring messages are only processed once.
- **Write Overhead**: Higher compared to other systems due to persistent message storage and delivery acknowledgment.
  
### 📝 Key Highlights
- Ideal for **task queues** and **service integration** scenarios.
- **Acknowledgment-based delivery**: Message is only deleted after consumer acknowledgment.
  
---

## 🦋 Kafka
- **High-throughput, low-latency message broker** optimized for real-time data streaming.
- **Write Efficiency**: Minimal overhead since data is logged sequentially, leveraging OS caches for recent messages.
- **Scalability**: Kafka’s partitioned log structure enables millions of messages per second with horizontal scalability for producers and consumers.

### 🚀 Performance Features
- **Partitioned Log Structure**: Producers can write to different partitions (e.g., Partition 0, Partition 1), enabling **parallel processing**.
- **High Throughput**: Kafka can achieve millions of messages per second by efficiently managing OS caching for recent messages.
- **Horizontal Scalability**: Both producers and consumers can scale out by adding partitions.

### ⚖️ Trade-offs
- **Limited Global Ordering**: Only guaranteed within partitions, not globally.
- **Consumer Pull Model**: Consumers pull data rather than receive pushed notifications.
- **Not Ideal for Service Integration**: Primarily used for streaming analytics and high-throughput workloads, such as:
    - Clickstream analysis
    - Real-time logging and ingestion
    - Security event monitoring

---

## 🔥 Redis Pub/Sub
- **Fast, lightweight messaging** for short-lived messages without persistence.
- **Message Lifecycle**: Operates in a fire-and-forget mode; messages are ephemeral and not stored after delivery.
- **Connection**: Maintains a long-lived TCP connection.

### 💡 Use Cases
- Best suited for **dashboard updates** or real-time leaderboards, where immediate visibility is essential.
- **Performance**: Capable of handling millions of operations per second.

### 🔄 Comparison with Kafka and RabbitMQ
- **Kafka**: Persistent, log-based storage with pull-only model.
- **RabbitMQ**: Message persistence and acknowledgment-based deletion after delivery.
- **Redis Pub/Sub**: No message persistence; suitable for transient, real-time updates.

---

Each system has unique strengths suited to specific scenarios:
- **RabbitMQ** 🐰: Great for task queues with reliable message delivery.
- **Kafka** 🦋: Ideal for high-throughput data streaming.
- **Redis Pub/Sub** 🔥: Best for transient, high-speed message updates without persistence.
<img width="1036" alt="image" src="https://github.com/user-attachments/assets/57c6860d-629f-47b7-8e6b-615c6922c4f6">

