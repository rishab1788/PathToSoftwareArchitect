
# 🔑 Symmetric Key

**Limitation**:  
The key needs to be shared with untrusted clients, which means it can't be shared with everyone.  

✅ With this, we achieve **privacy/confidentiality**.

---

# 🔐 Public Key Encryption (Asymmetric Key)

In **Public Key Encryption**, we have a **public key** and a **private key**. They form a pair, and both are needed for encryption and decryption.

```plaintext
            [Public Key]               [Private Key]
Plain Text ----> Encrypted Text ---> Plain Text
```
- Only the **intended recipient** with the private key can access the data.  

```plaintext
           [Private Key]                 [Public Key]
Plain Text ----> Encrypted Text ---> Plain Text
```
- Ensures the **identity of the sender** and the **integrity** of the data.

---

# 🌐 Secured Network Protocol (SSL/TLS)

When setting up a secure connection, **SSL** (Secure Sockets Layer) and **TLS** (Transport Layer Security) protocols are used. These provide secure communication over a network. 

📢 Note: **TLS** is the successor of **SSL**, with SSL being deprecated due to security vulnerabilities.

### 🔑 How SSL/TLS Works (From a Backend Developer's Perspective)

1. **Establishing a Secure Connection**  
   When a client (like a web browser) connects to a server, the **SSL/TLS handshake** begins to establish a secure session.

2. **The SSL/TLS Handshake**  
   The handshake process involves the following steps:

### 🖐️ Step 1: Client Hello
The client starts by sending a **"Hello"** message, which includes:
- Supported **SSL/TLS versions**.
- A list of supported **cipher suites** (encryption algorithms).
- A randomly generated number for session key generation.

### 🖐️ Step 2: Server Hello
The server responds with its own **"Hello"**, containing:
- The chosen **SSL/TLS version**.
- The chosen **cipher suite**.
- The server’s **digital certificate** (X.509), which includes the **public key**.

### 🔑 Step 3: Certificate Verification
The client verifies the server’s certificate:
- Is it **valid**?
- Is it issued by a trusted **Certificate Authority (CA)**?  
If valid, the client proceeds.

### 🔄 Step 4: Key Exchange
The client and server agree on a shared **session key** for encrypting communication.
- In modern TLS, **Elliptic Curve Diffie-Hellman (ECDHE)** is often used for secure key exchange.

### 🔑 Step 5: Session Key Creation
Both the client and server use the chosen method (like Diffie-Hellman) to independently generate the same session key—without exchanging the key itself over the network.

### 🔐 Step 6: Secure Communication
Once the handshake is complete, both client and server use the **session key** to:
- **Encrypt** and **decrypt** all further communication.  
This is done using **symmetric encryption**, which is faster than the asymmetric encryption used during the handshake.

---

# 🔢 Hashing for Secure Communication

🔑 **Hashing** is a process that converts input into a fixed-length **hash output**. It is a **one-way algorithm**:
- Always generates the same hash for the same input.
- Even the slightest change in input drastically changes the hash.
- **Collisions** (where two inputs produce the same hash) are rare with modern algorithms.

### Popular Hashing Algorithms:
- **MD5**: 128-bit hash.
- **SHA-1**: 160-bit hash.
- **SHA-2**: 256/512-bit hash.
- **SHA-3**: Newer variant of the SHA family.

---

# 🖊️ Digital Signatures

Digital signatures ensure **integrity**, **authentication**, and **non-repudiation** of a document.

- The data is **hashed**.
- The **signer** uses their **private key** to sign the hashed message.
- The recipient uses the **public key** of the signer to verify the signature.  
- The message is hashed independently by the recipient and compared with the hash in the signature.

---

# 📄 Digital Certificates

Digital certificates provide a **trusted** way of sharing a public key with the world.  
- They ensure that **any client** can verify the ownership of the public key.


# 🛡️ Hashing and Network Security Concepts

## 🔒 Hashing
Hashing is used for secure communication by converting input data into a fixed-size hash output. It's a one-way algorithm, meaning:
- Same input always produces the same output.
- The slightest change in the input drastically alters the hash value.
- Hashing ensures data integrity.

### 🚀 Popular Hashing Algorithms:
- **MD5**: 128 bits
- **SHA-1**: 160 bits
- **SHA-2**: 256 and 512 bits
- **SHA-3**: Latest in the series.

## ✍️ Digital Signatures
Digital signatures ensure **integrity**, **authentication**, and **non-repudiation** of a document.

1. Data Document 📝 → Hash is generated 🔑
2. The signer uses their **private key** to encrypt the hash.
3. The recipient uses the signer’s **public key** to verify the message and the hash.

## 🌍 Digital Certificates
A way to share a **public key** with the world in a trusted manner. They ensure any client can verify who the public key owner is.

## 🔗 Chain of Trust
1. **End-Entity Certificate**: Identifies the owner of the certificate.
2. **Owner’s Name**: Details of the certificate holder.
3. **Owner’s Public Key**: Public key of the certificate holder.
4. **Issuer (CA)**: Certificate Authority that validates the certificate.

## 🌐 Secured Network Channel (SSL/TLS)
- Certificates and keys are deployed on external load balancers for secure communication.
- **Why TLS?**: 
  - TLS ensures encrypted communication over the internet.
  - Without TLS, data can be viewed and understood by anyone who can access the network.

### 🛑 Firewalls
Firewalls act as **filters** to allow or deny network requests:
- **Ingress Filtering** (incoming traffic):
  - Source IP, Target IP, Target Port, Protocol (TCP/UDP)
- **Egress Filtering** (outgoing traffic):
  - Destination IP, Target IP, Target Port, Protocol

## 🔐 Network Security
Typical network setup:
- **DMZ Subnet 1**: Port 443
- **DMZ Subnet 2**: Port 443 (Internal hosts)
- **Services Subnet**: Port 8080 (Aggregator service)
- **Database Subnet**: Port 1522

## 🆔 Identity Management

### 🔑 Authentication (Who You Are)
- Proving an identity:
  - **ID**
  - **Name**
  - **Organization**

### 🚦 Authorization (What You Can Do)
- Proving the right to access specific functions/services.
- Ensures controlled access to data.

### 🔗 Credential Transfer
- **HTML Forms**: HTTP Post Method over SSL/TLS.
- **HTTP Basic**: Base64-encoded credentials transferred over SSL/TLS.
- **Digest-based**: Hashed password for verification.
- **Certificate-based**: Uses private-public key pairs for exchange.

## 🔐 Credential Storage & Verification

### 🗂️ Storage Methods:
1. **File Storage**: Not scalable.
2. **Database**: RDBMS or NoSQL databases.
3. **LDAP**: Lightweight Directory Access Protocol, ideal for high-read environments and enterprise setups.

## 💾 Stateful Authentication
- Session-based, centralized authentication.
- Sessions can be revoked by removing them from the session storage.
- Common cache is used to store session values for scalability.
