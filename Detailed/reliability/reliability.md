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
