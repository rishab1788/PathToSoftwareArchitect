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

 
 

# 🛠️ Fault Tolerant Design

In a distributed system, achieving fault tolerance is crucial to ensure the system continues to operate correctly even when partial failures occur. Let’s break down how fault detection, monitoring, and health checks are applied.

---

## 🔍 Fault Detection

Fault detection is about identifying when a component of the system is not functioning as expected. It is done by continuously monitoring the system's health and behavior.

---

## 📉 Fault Models

Understanding different types of failures helps in designing effective fault-tolerant systems.

1. **Response Failure**: 
   - A server fails to receive or respond to incoming messages.
   - 🛑 **Symptom**: No response.

2. **Timeout Failure**: 
   - A server’s response takes longer than the expected timeout duration.
   - ⏳ **Symptom**: Response delay beyond allowed time.

3. **Incorrect Response Failure**:
   - A server responds with an incorrect result.
   - ⚠️ **Symptom**: Incorrect data returned.

4. **Crash Failure**:
   - The server stops functioning entirely after working correctly for a period.
   - 💥 **Symptom**: Complete halt of the service.

5. **Arbitrary Response Failure** (also called Byzantine failure):
   - A server’s response is incorrect due to compromised security or internal faults.
   - 🚨 **Symptom**: Malicious or faulty data returned.

---

## 📊 Health Checks

**Health checks** are essential tools for monitoring the status and functionality of system components. They can detect failures and initiate recovery mechanisms.

### 🔧 External Monitoring Service

- **Monitoring Service** constantly "pings" your servers:
  - 🏓 **Ping**: Sending periodic checks to confirm the system’s availability.
  - 🛡️ **Goal**: Ensure services are reachable and functioning properly.

### 💓 Internal Cluster Monitoring

- **Heartbeats**: Periodic signals exchanged between nodes in a redundancy cluster to ensure they're functioning properly.
  - Useful for **stateful** and **clustered** components to detect partial or complete failures.

---

## 🚨 External Monitoring Service

An external health check service monitors the system and responds accordingly:

### 🛎️ Health Check Service Generates:

1. **Alerts**: 
   - 🛠️ Used to notify administrators or systems of issues that need recovery.
   
2. **Events**:
   - 📈 Triggered to handle system scaling based on monitored performance.
   
### 🚥 Application Health Checks

Health checks monitor different parameters of a service:

1. **HTTP Response**: 
   - 🖥️ Ensures that web services are responding correctly.
   
2. **TCP Response**: 
   - 🔌 Monitors server connectivity through established protocols.

### ⏱️ Periodic Health Checks

Performed regularly to keep track of the system's health:

- **Response Code**: Expected HTTP status codes (e.g., 200 OK).
- **Response Time**: Monitor latency and ensure it is within acceptable limits.
- **Number of Retries**: 
  - If multiple retries are needed to get a response, it could be a sign of service degradation.
  - ⚠️ Status: **UP** (service running smoothly) or **DOWN** (service unavailable).

**Public Cloud** makes it easy to implement periodic health checks.

---

## 🧐 What Happens if the Monitoring Service Fails?

When the **monitoring service** itself is down, it poses a significant challenge. One solution is to have a **Health Check Service** to monitor the monitoring service itself!

---

## 🤝 Inter-Cluster Monitoring

- **Heartbeat Exchange**: Periodic heartbeats are exchanged between nodes in a redundancy cluster to ensure all nodes are functioning.
- **Communication Protocols** are necessary for recovering from failures.
- **Useful for Stateful Components**: 
  - In **stateful** systems, the cluster needs to coordinate closely for fault detection and recovery.

---

## 🚦 Fault Detection Monitoring Techniques

1. **Health Checks**:
   - Commonly used in stateless services.
   - 🎯 Focus: Check service health at predefined intervals.

2. **Heartbeat Monitoring**:
   - Used in cluster-based systems where nodes monitor each other.
   - 💓 Focus: Ensure that nodes remain active and synchronize state.



# ⚡ Stateless and Stateful Recovery Mechanisms

## ⚙️ Stateless Recovery

Stateless recovery leverages the existing scalability mechanisms for recovery. Since stateless services don’t store session data locally, they are more flexible in terms of recovery strategies.

### 🔥 Hot Standby
- **Active redundant instances** are kept up and running.
- In the event of failure, the system can quickly switch over to the redundant instances with minimal downtime.

### 🛠️ Warm Standby
- **Bring up new instances** as needed when failure occurs.
- **Terminate unhealthy instances** that aren’t functioning, and launch a new instance in its place.

    [Load Balancer ] ----> 1,2,3, ---> Monitoring and Health check () --> autoscaler -> VM container/image.

Stateful failover

    Virtual IP                   
  client-> DNS(10.2.2.2)
      floatingIP
            |
 primary -HeartBeat-   standby
(192.1.1.1) (192.2.2.2)

Registry/Router/DNS
      Client --> Registery --> Instance 2
       |         
    instance1

 
Database Recovery - Hot StandBy 
Master -> Slave 
Master -> master setup can result to write conflicts so they have very specifc usecase.
Incase of downtime we want almost no downtime
No data loss 

    [Client]
    |
    |
    Primary(X)-----------> Secondary
    Instance-1             Instance-2
    Then secondary can we switched 
    can start service updates.
  Both primary and secondary will be near by so that lag can be reduced.
  
proximity needed 
Slow DB writes 

Database recovery - Warm Standby setup
  Asynchronous Replication 
  Catchup before recovery
  Possibility of lost updates 
  
          [Client]
      |
      |
      Primary(X)----Async-------> Secondary
      Instance-1                  Instance-2
        Log 1                      Log 2 
        Then secondary can we switched 
        can start service updates.
  
  High Performance 
  Disaster Recovery 
  we use this incase of Disaster recovery, the enitire datacenter can go down thats why we use async.


💡 **Key Concepts**:
- **Hot Standby**: Immediate availability and minimal recovery time.
- **Warm Standby**: Slower to recover but reduces the cost of running idle instances.
- **Stateful Failover**: Ensures data is synced between the primary and standby servers to allow seamless failover.  



# 📊 Database Recovery (Cold Recovery)
- **Based on DB Backups**  
  - 🏷️ **Cost-Effective**  
  - 🕒 **Significant Downtime**  
    - Recovery from backups involves a longer downtime, as the system must be fully restored from the latest backup.
  
- **DB Corruption**  
  - Replication does not help when corruption is present because it can propagate the corrupted data.
  
- **Recovery Process**  
  - 📜 **Log Updates**  
  - 💾 **Backups**  
    - Regular **checkpoint** systems should be in place to ensure consistent recovery points.
  - 📥 **Import**  
    - Import the necessary backup data.  
  - 🔄 **Apply Updates**  
    - Replay the transaction log updates to get the database back in sync.

---

# 🌍 High Availability in Large-Scale Systems
![High Availability](https://github.com/user-attachments/assets/4638cac8-45bd-49ab-99dd-9c0d0e58524e)

### How to Maintain Consistency Across Regions  
- The challenge is ensuring data consistency across geographically distributed regions.  
- **Master-Master Replication**: Ensures each region has writable databases and consistent data.  
- **Synchronous Replication** between nearby data centers (e.g., Mumbai1 and Mumbai2).  
- **Asynchronous Replication** for geographically distant locations (e.g., between Mumbai and Singapore) due to network latency.

### 🛠️ Failover Best Practices
- **Failover Automation**  
  - Automating failover systems ensures rapid recovery without human intervention.
  
- **Regular Failover Testing in Production**  
  - Continuously test your failover mechanism in a live production environment to ensure preparedness.

---

# ⚙️ System Stability
### Approaches for Severe Load Handling:
#### 1. **Timeouts**
   - 🕒 **Client Components**  
     - **User Interface**  
     - **Service Clients**  
   - Timeouts prevent calls from being blocked due to long waits, avoiding cascading failures.
   - Example:  
     - `Client --> ServiceA --------------> Service B1(X)`

#### 2. **Retries**  
   - Retrying for **transient failures** and **system errors**, but **not application errors**.  
   - 🌀 **Exponential Back-off**  
   - 🔁 Return `HTTP 503` to let clients decide when to retry.  
   - Use **Idempotent Tokens** to guarantee at least one request is processed, instead of exactly once.

#### 3. **Circuit Breaker**  
   - Prevents continuous failures by stopping requests to failing components when failure conditions are met.

![Circuit Breaker](https://github.com/user-attachments/assets/1588a6e1-654e-49bb-8e62-113c49cce60b)

---

# 🚨 Fail Fast & Shed Load
### **Server Components**
- **Fail Fast**  
  - Triggered when a component is unable to process requests.  
    - 🧪 Validation errors  
    - ❌ Missing parameters/environment variables  
    - ⏳ Service timeouts (when circuit breakers are active)  
  - The component should return an error as soon as possible upon discovering failure.
  
- **Shed Load**  
  - Failing fast due to external load beyond system capabilities.
    - 💻 **Concurrency Limits**: Control thread counts, connections, and request numbers.  
    - 🔄 **SLA**: If service level agreements (SLA) are breached, incoming requests should be blocked or rejected.
  
- **Back Pressure**  
  - Apply back pressure by shedding load to slow down clients within system boundaries.

 
