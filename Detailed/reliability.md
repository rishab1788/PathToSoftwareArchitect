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

