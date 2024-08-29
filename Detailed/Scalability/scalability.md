# 🚀 Scalability Overview

## 📈 Vertical & Horizontal Scaling

### 🌐 Horizontal Scalability
- 📊 **Replication**
- 🛠️ **Services**
- 💾 **Caching**
- 🔄 **Asynchronous Processing**
- 📑 **Partitioning**

## ⚖️ Load Balancing
- ⚙️ **Load Balancer**
- 🔍 **Service Discovery**
- 🌍 **DNS & Geo Load Balancing**

## 🧩 Micro-Services
- 🏗️ **Architecture**
- 💳 **Transactions**
- 🔄 **SAGA Pattern**
- 🗃️ **NoSQL**


# 🚀 Scalability Overview

## ⚖️ Performance vs Scalability

### ⚡ Performance - Fixed Load
- ⏱️ **Low Latency**
- 📈 **High Throughput**
  - Concurrency
    - 💻 Single Machine - Multithreading
    - 🖥️ Multi Machine - Multithreading + Multi-Processing = Distributed Processing
  - 🛠️ **Capacity**

### 📊 Scalability (Subset of Performance) - Variable Load
- 📈 **High Throughput**
  - Ability of a system to increase its throughput by adding more hardware capacity.
  - Scalability works both ways - Up and Down.

## 📈 Vertical & Horizontal Scalability

### 📏 Vertical Scaling
- Easier to achieve.
- Limited scalability.
- Example:
  - Initial: [Web Browser] ----> [CPU (4 CPU, 16 GB RAM)]
  - Scaled: [Web Browser] -----> Scaled---> [CPU (32 CPU, 256 GB RAM)]

### 🏗️ Horizontal Scaling
- Harder to achieve.
- Unlimited scalability.

## 🔄 Reverse Proxy
- Clients need to know only about the address of the reverse proxy.
- Reverse proxy can also act as a load balancer.

Example:
  - [Web Browser] --> [Server1/IP-10.222.22.11]
  - [Web Browser] --> [Server2/IP-10.222.22.12]
  - [Web Browser] --> [Server3/IP-10.222.22.13]

Example with Load Balancer:
  - [Web Browser] --> (Load Balancer (proxy/DNS name)) --> |--> [Server1/IP-10.222.22.11]
                                                           |--> [Server2/IP-10.222.22.12]
                                                           |--> [Server3/IP-10.222.22.13]

## 🔑 Scalability Principles

  ### 🔓 Decentralize
  - Monolith is an anti-pattern for scalability.
  - More workers - instances, threads.
  - Specialized workers - services.
  
  ### 🔄 Independence
  - Multiple workers are as good as a single worker if they can't work independently.
  - Workers must work concurrently to the maximum extent.
  - Independence is impeded by:
    - Shared resources.
    - Shared mutable data.
  
  ### 🧩 Modular Architecture
  - Start with modular code to achieve scalability.
  
  ## 🔁 Replication - Handling Increasing Workloads
  
  # 🖥️ Stateless (Service)
   - **Code replication**.

# 🗄️ Stateful (Mostly DB)
   - **Code & Data replication**.

## 🌐 Web Stateful Replication 
- When **Low Latency** is required:
  - 🔄 **Sticky session/session affinity**.
  - 🧠 **Session occupies memory**.
  - 🛡️ **Session clustering for reliability**.

## 🌐 Web Stateless Replication (Preferred)
- For the **highest scalability** at the expense of higher latency:
  - ⚡ We can use **memCache/Redis** which all nodes share, decreasing latency.
  - 🗃️ **Session data can be stored**:
    - On the **Client Side** in cookies 🍪.
    - On the **Server Side** in a **Shared Cache**.

## 📡 Service Replication
- **Stateless Replication**: Same as Web Stateless.
- Use **DB Lock 🔒**.

# 🛢️ Database Replication
- Used when **Vertical Scaling** is no longer sufficient.
- For **High Read Scalability 📈**.
- For **High Availability 🟢**.

### RDBMS (Relational Database Management System) - 🛠️ General Purpose
### NoSQL - 🛠️ Specific Use Cases

### RDBMS Scaling
- When the RDBMS is **overloaded**, we create a **Read Replica** (Master/Slave):
  - Another DB instance is created. What’s written in the **Master** gets replicated to the **Slave**.
  - We can create multiple read replicas for handling more read requests.

- **Backup Database**:
  - Created for a different purpose.
  - Used when the **Master** goes down, and the **Backup** gets replaced.

## 🔀 Two Ways to Perform Database Replication
# Database Replication Strategies

## 1. **Master-Slave (Primary-Secondary) Replication**
### 🕒 Asynchronous - (Read Replica)
- **Use Case:** When low latency reads and writes are required.
- **Characteristics:**
  - ⚡ Low Latency
  - 🔄 Eventually Consistent
  - ⚠️ Potential for Data Loss

### 🔄 Synchronous - (Backup)
- **Use Case:** When a reliable backup is needed, typically with 4-5 read replicas where 1 backup replica remains in sync.
- **Characteristics:**
  - ✅ Consistent Data
  - 🕑 High Latency Writes
  - 📉 Low Write Availability (Writes become unavailable if a node is down)

## 2. **Master-Master (Peer-to-Peer) Replication**
- **Description:** Data is replicated with a slight delay. This method is not very popular but can be useful in global regions, with the understanding that write conflicts and transaction ordering issues may occur.
- **Characteristics:**
  - 🏢 Both databases act as masters, allowing reads and writes on both instances.
  - 🔄 Bidirectional replication between nodes.
  - ⚠️ Potential for write conflicts due to asynchronous replication.
  - 🔄 High Availability.

## Need for Specialized Services
- **Requirement:** Only applicable if we can break our monolithic application into smaller, manageable services.
- **Challenge:** If all modules remain in one system and only one part of a module needs updating, replicating all modules would increase load and create potential issues.

### Specialized Services (SOAP/REST)
- 🛠️ **Partially Independent Development and Deployment**
- 📈 **Independent Scalability**
- ⚙️ **Independent Technology Choices**

- **Aggregator Service or Gateway Service**: 
  - Required to help in redirecting traffic to different modules.
  
- **Interoperation Interface**: 
  - For inter-module communication, we can use REST, SOAP, gRPC, or Thrift.

- **Where to use async services**: 
- They are best suited for write-oriented operations where data does not need to be immediately shown to the user.
- Not ideal for read-heavy request models.
- They offer flexibility, allowing the system load to be scaled up or down.

- **Asynchronous Processing & Scalability**:
- Async services require infrastructure designed for average load rather than peak load.
- By adding a message queue (MQ) for orders and an order processing service that makes actual DB changes at average load, we can avoid overloading the database.
- This approach removes the need to reject requests during peak times.

- **Benefits**:
- 🗂️ Reduces over DB capacity.
- ✅ Ensures that requests don't have to be rejected.

# Caching 🗄️

- **Caching** reduces latency and overall read load:
- HTTP Cache, Session Cache, Object Cache.
- While read load can be scalable, scaling write load on a database is more complex.
- **Cache** helps to reduce read load, while **Asynchronous Services** help to reduce write load.

# Vertical Partitioning (Microservices) 🏗️

- As load increases, both database load and service demands increase. RDBMS cannot be distributed easily.
- Example: Order Service, Catalog Service, User Service -> Independent services with clear-cut data separation, allowing for separate databases.
- One database can be refactored into multiple databases (e.g., four DBs). If there are common tables, they must be split.
- **Separation of responsibilities**: This improves the situation but sacrifices the ACID transaction model.

- **Microservices Architecture**:
- This architecture is also known as microservices architecture, where each service has its own database.
- Examples:
  - 🧑‍💼 [User Service] -> [User DB]
  - 📦 [Order Service] -> [Order DB]
  - 📚 [Catalog Service] -> [Catalog DB]

# Database Partitioning and Horizontal Scaling 🌐

## Database Partitioning 🗃️

When scaling databases, vertical partitioning has its limits, which is where horizontal partitioning (or sharding) comes in. Horizontal partitioning divides a database into smaller, more manageable pieces. Here are the two common types:

### 1. Range Partitioning 📊
- **Description**: Data is divided into partitions based on ranges of values.
- **Example**:
  - Partition 1: `[1..1000]`
  - Partition 2: `[1000..2000]`
  - Partition 3: `[2000..3000]`
- **Use Case**: Ideal for queries that involve ranges. For example:
  ```sql
  SELECT * FROM orders WHERE id > 150 AND id < 250;


    where can we use Range Partitioning and Hash Partioning 
    SQL example - 
      Select * from order where id = 150
      Select * from order where id > 150 AND id < 250
      visit node 1 and node 2

      Select * from order where id = 150. // then use Hash partitioning.
      
      Range Partitioning uses tree structure but hash just do it O(1)  
      
Routing with Database Partitioning 

GET- 256
                        [1,100]
  [Client Library] ---> [100,200]
                        [200, 300]

## 🗂️ Summary of Horizontal Scaling Methods

1. **Services**: Decomposing the application into smaller, independent services.
2. **Replication**:
   - **Stateful**: Replicates both code and data.
   - **Stateless**: Replicates code only; data is managed separately.
3. **Partitioning**:
   - **Vertical/Functionality Partitioning**: Divides based on functionality.
   - **Database Partitioning**: Uses range or hash partitioning to distribute data.
4. **Asynchronous Calls**: Handles operations asynchronously to enhance scalability.
5. **Caching**: Reduces latency and load by storing frequently accessed data in memory.

## 🌐 Dealing with Large Scale Systems

### ⚖️ Load Balancing
- **Single IP Address**: Assigns a single IP address to each component.
- **Load Distribution**: Distributes incoming requests across multiple instances to balance the load.

### 🔍 Discovery Service & Load Balancing
- **Discovery Service**:
  - **Function**: A registry for tracking healthy instances of services.
  - **Process**: Services register with the discovery service and periodically send heartbeats to indicate availability.
  - **Example**: When an `OrderService` instance (`O1` or `O2`) starts, it registers with the discovery service. The service then directs traffic based on load balancing strategies.

  **Discovery Service Details**:
  - **Registry**: Keeps track of IPs and health statuses of instances.
  - **Heartbeat**: Services periodically send a heartbeat signal to confirm they are available.
  - **Load Strategy**: Traffic routing is based on the load balancing strategy defined.

---
