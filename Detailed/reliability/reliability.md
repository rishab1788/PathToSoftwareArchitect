# 🌐 System Reliability

## 🚀 Horizontal Scaling & Distributed Systems

- **Availability**: Ensuring the system is always up and running.
- **Reliability**: The system performs as expected consistently.
- **Fault Tolerance**: The ability to continue operation despite failures.
- **Partial Failures**: Handling situations where parts of the system fail without affecting the whole.

## 🛠️ Designing Fault Tolerance

### 🔄 Redundancy
- **Hot**: Immediate failover with zero downtime.
- **Warm**: Ready to take over with minimal downtime.
- **Cold**: Needs manual intervention and time to take over.

### 🩺 Fault Detection
- **Health Checks**: Regularly verifying the system’s components are working properly.
- **Monitoring**: Continuous observation to detect issues early.

### ♻️ Recovery
- **Stateless**: Easier to recover since no state is held within the service.
- **Stateful**: More complex recovery due to the need to maintain state.

## ⚖️ System Stability

### ⏳ Timeouts
- Avoid hanging requests by implementing timeouts.

### ⚠️ Circuit Breakers
- Prevent cascading failures by stopping requests to failing services.

### 🏃‍♂️ Fail Fast & Load Shedding
- Quickly fail requests when a problem is detected to avoid overwhelming the system.

---

# 🛑 Failures in Large-Scale Systems

## 🌍 Characteristics of Large-Scale Systems
- **Distributed Systems**: Spread across multiple locations or machines.
  - **Large Number of Components**: Multiple services and machines involved.
  - **Independent Failures**: Components can fail independently.
- **Single Point of Failure**: Identifying and eliminating single points of failure is crucial.

## ⚡ Increased Risk of Partial Failures
- **Partial Failures**: Can lead to complete system failure if not handled correctly.

### 🔍 Types of Partial Failures

#### 🌐 Network Failures
- LAN, WAN, Load Balancer issues.

#### 💻 Machine Failures
- CPU, Disk, Memory malfunctions.

#### 🛠️ Software Failures
- Process crashes or bugs.

#### 🌪️ Disasters
- Data center outages.

#### 🔧 Operational Failures
- Deployment errors, configuration mistakes, load-induced failures, external service issues.

---

## 💡 Key Takeaways
- After a certain point, it's more economical to **recover** from failures than to **prevent** them entirely.
- **Hardware** and **networks** will inevitably fail, and software changes can introduce bugs.
- Disasters are unpredictable but inevitable.
- We should design systems that can **recover** from failures rather than attempting to prevent them entirely.


# 🚀 Reliability Engineering

### Core Concepts:
* **Reliability**, **Availability**, **Fault Tolerance**.

### 📈 Reliability
- A system is said to be reliable if it can continue to function correctly and remain available for operation, even in the presence of partial failures.
- 🛩️ **Example**: If an airplane loses one engine but still operates normally, it demonstrates reliability.
- Reliability is measured as the **probability of a system working correctly** over a given time interval.

### 🕒 Availability
- Availability refers to the **probability of a system working correctly** at any given time and being available for operations.
- **Time-based Availability**: 
Availability = Uptime / (Uptime + Downtime)

 Availability = (Successful Requests / Total Requests) * 100%
- **Request-based Availability**: 

- 🔄 Even if there's downtime, the system is expected to **recover quickly**.
- **High Availability**: It's difficult to achieve 100% availability, but systems like ATMs aim for 99.999% availability, which translates to just **5 minutes of downtime per year**.

#### Availability Requirements:
| Availability  | Max Disruption     | Application Categories                         |
| ------------- | ------------------ | ---------------------------------------------- |
| 99%           | 3 days 15 hours     | Batch Processing, Data Extraction              |
| 99.9%         | 8 hours 45 minutes  | Internal Tools (e.g., Knowledge, Project Tracking) |
| 99.95%        | 4 hours 22 minutes  | Online Commerce, Point of Sale                 |
| 99.99%        | 52 minutes          | Video Delivery, Broadcast Systems              |
| 99.999%       | 5 minutes           | ATM Transactions, Telecom Systems              |

💡 Systems should use permitted **downtimes** in their SLA/SLO for **planned rollouts** and updates.

---

## ⚙️ Fault Tolerance
- Fault tolerance is the **technique used to improve availability and/or reliability** of a system.
- It refers to a system's ability to automatically:
- 🛠️ **Detect partial failures**
- 🛠️ **Handle partial failures**
- 🛠️ **Recover from partial failures**
- **Serviceability**: The ease with which a system can be serviced in the event of a failure also contributes to its availability.

---

## 🛡️ Designing Fault Tolerance
- **Redundancy** → **Fault Tolerance** → **Recovery**

### 🔁 Redundancy
- **Redundancy**: Duplication of critical components/functions to enhance reliability.
- Backup capacity is kept ready in case the primary system fails.

#### Types of Redundancy:

1. **🟢 Active Redundancy** (Hot Spare):
 - All nodes are active and process data simultaneously.
 - Ideal for providing **highest availability**.
 - **Example**: In load balancing, two systems handle 50% of the load. If one fails, the other takes over 100%.
 - **Advantage**: Very fast and efficient in ensuring availability.

2. **🟡 Passive Redundancy** (Warm Spare):
 - Only active nodes process the data.
 - Backup nodes are **ready to take over quickly** when needed.
 - **Example**: Similar to how substitute players are ready to jump in when one player is injured.

3. **🔴 Cold Redundancy** (Cold Spare):
 - Spare nodes are brought online only in the event of a failover.
 - Not ideal for **high availability** as it takes time to recover.

# 🚨 Single Point of Failure (SPOF)

In any system, a **Single Point of Failure (SPOF)** refers to a component whose failure could lead to the failure of the entire system. Let's explore ways to mitigate SPOF risks through redundancy and fault tolerance.

---

## 🖧 Key Components Leading to SPOF

### Load Balancer, Message Queue, Discovery Service
- If we don't provide **redundancy** for these components, they could become SPOFs.
- To ensure high availability, we need to implement redundancy for each.

---

## 🟢 Redundancy for Stateless Components

- **Stateless components** are easier to scale by creating replicas.
- Replicas are deployed in an **Active-Active** manner for redundancy.
- **Examples**: Web applications, microservices.
- **Scaling**: We need to ensure we have enough replicas to handle the expected load.

---

## 🟡 Redundancy for Stateful Components

- **Stateful components** such as databases, message queues, caches, and static content **require redundancy** to keep data in sync.
  
### 🗄️ Database Redundancy:
- **Master-Secondary Architecture**: 
  - [Inventory Service] ➡️ **Master DB** (syncs data) ➡️ **Secondary DB**.
  - This can be done via **synchronous** or **asynchronous replication**.
  - Active-Active setups are very fast, ensuring **high availability**.

### 📮 Message Queue Redundancy:
- Redundancy for message queues typically follows a **Primary-Secondary** model.

### 🗂️ Static Content Redundancy:
- **Handled by vendors**: Redundancy for static content (images, videos) is generally managed by third-party vendors (e.g., CDNs).
  
### 🛠️ Cache Redundancy:
- **Cache Services** can be:
  - **Static or Dynamic** in nature.
  - Some cache services don't require redundancy (e.g., Memcached), as a cache miss is acceptable.
  - **Redis** provides built-in redundancy options.

---

## ⚖️ Load Balancer Redundancy

- A **Load Balancer** can be a **critical SPOF**. Hence, redundancy is crucial:
  - We set up **Primary** and **Secondary** load balancers to ensure seamless failover.

---

## 🏗️ Infrastructure as SPOF

### 🛜 Local Area Network (LAN):
- **Multiple Internet Connections**: Data centers often have multiple connections to the internet to prevent network failures from becoming SPOFs.

### 🏢 Data Center Redundancy:
Data centers themselves can be vulnerable to failures due to natural disasters, such as floods or earthquakes. Therefore, it's essential to design for **data center redundancy**.

#### 🛡️ Fault Isolation:
- Independent infrastructure across data centers ensures that issues in one center don’t cascade to others.

#### 🏙️ Zonal Redundancy:
- **High Availability** via an **Active-Active Setup**.
- Having two data centers at least **10 km apart** ensures that one can continue operations if the other fails.

#### 🌍 Regional Redundancy:
- **Disaster Recovery** through an **Active-Passive Setup**.
- The passive data center will take over only when the active one fails.

 
 
