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
 
