
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



# Role-Based Access Control (RBAC) 🚀

RBAC is a method to restrict system access to authorized users based on their roles. It simplifies the management of user permissions by associating a role with a set of permissions, which is then assigned to users or user groups. This is commonly used in enterprise applications to enforce fine-grained access control.

### Key Concepts 🔑

- **Identity** 👤
  - **User ID**: Represents the user in the system.
  
- **Identity Group** 👥
  - **Set of User IDs**: A group that aggregates multiple users for easier management.

- **Permission** ✅
  - **Allowed Operation**: Defines the specific actions a user can take (e.g., read, write, update).

- **Role** 🎭
  - **Set of Permissions**: A role bundles a collection of permissions that users in that role can execute.

- **Resource** 🔧
  - **Service API**: The system or service endpoints that users interact with.

---

## Example Access Control Flow:

```java
doFilter(request, response) {
   authHeader;      // Get authorization header from request
   authToken;       // Extract authentication token
   auth;            // Validate authentication (OAuth2, API Key, etc.)
   role;            // Get user's role (Customer, Manager, etc.)
   resourceMethod;  // Determine the requested resource (e.g., Read Catalog)
   requiredPermission;  // Identify the permission required (e.g., CATALOG_VIEWER)
   role.hasPermission(requiredPermission);  // Check if the user's role allows the requested action
}
```

Annotations for securing resources:
```java
@Secured{Permission.CATALOG_VIEWER}  // Restrict access to users with CATALOG_VIEWER permission
```

### Example Roles, Permissions, and Users 🧑‍💻

| **Users** | **Groups**  | **Roles**        | **Permissions**         | **Business Resource**  | **System Resource**         |
|-----------|-------------|------------------|-------------------------|------------------------|-----------------------------|
| Alice     | Customer    | Customer Role    | Read Catalog             | Order Service           |                             |
| Carol     | Support     | Support Role     | Read Inventory           | Catalog Service         |                             |
| Eve       | Inventory   | Manager Role     | CRUD Catalog             | Inventory Service       | Inventory Database          |

---

## Authorization Mechanisms 🔓

### OAuth2 🔑
OAuth2 is designed for distributed systems, allowing a client to access a protected resource on behalf of a resource owner. 

- **Token Grant**: OAuth2 allows clients to request access tokens for API requests using different types of grants (e.g., Authorization Code, Client Credentials).
- **Token Types**: 
  - **Bearer Token**: Widely used for API authentication; whoever possesses this token can access the resource.
  - **MAC Token**: Message Authentication Code-based token offering a more secure, signature-based method of access.
- **Token Formats**: 
  - **JWT (JSON Web Token)**: A compact token format often used for stateless authentication.
  - **SAML (Security Assertion Markup Language)**: Commonly used in Single Sign-On (SSO) scenarios, especially in enterprises.

### API Key 🔐
- **Used by server applications** to authenticate requests.
- **Purpose**: To identify the origin of a request rather than the user making the request.
- **Validity**: API Keys are often restricted to specific domains or IP addresses.
- **Limitations**: They do not offer granular user-based control and are more suitable for server-to-server communication.

#### Example Use Case:
- Google Maps API requires an API key to access its services, but it doesn't care about who the user is—only the origin of the request.
# OAuth 2.0 Token Grant

### 🧑‍💻 Resource Owner
   * The **user** who has access to the resources.

### 🌐 User Agent
   * The user's **HTTP browser** used to access the client.

### 🛠 Client
   * An **application** that needs access to the user's resources.

### 🛡 Authorization Server
   * The **identity provider** responsible for authenticating users and issuing access tokens.

### 🗄 Resource Server
   * **Hosts the user's resources**.
   * Any client with a valid **access token** can access the user's resources.

---

## 🔑 OAuth Token Types

### 🎫 Bearer Token (Cinema Ticket Analogy)
   * Anyone who has the token can use it (like a cinema ticket).
   * Provides **integrity protection** only.
   * **Requires TLS** for confidentiality.
   * Supports **refresh tokens** to renew access.
   * **Expires** after a specified period.

### 🛂 MAC Token (Holder of the Key)
   * Issued to a specific person, requiring proof of identity (like an airline ticket).
   * Offers **data origin protection**.

---

## 🔐 JSON Web Tokens (JWT)

### 🔍 What is JWT?
   * A **JSON-based** token specification.
   * **Compact** and **URL-safe** for efficient transmission.

### 🧾 JWT Contains:
   * Information about:
     * **Subject or Principal** (e.g., the user).
     * **Issuer** of the token (e.g., the identity provider).
     * **Timestamp** (when it was issued).
     * **Validity** period and the **scope** of usage.

### 🛠 JWT Format:
   * `{Header}.{Payload}.{Signature}`
     * Signature is created by the identity provider.
     * Supported algorithms include:
       * `HS256` -> HMAC with SHA256
       * `RS256` -> RSA with SHA256
     * JWT **may or may not** be encrypted.

### 🔄 Alternative to JWT:
   * **SAML Tokens** (XML-based tokens).

---

## 🔒 Token Storage Best Practices

### 🖥 Web Client
   * **Browser Cookies**:
     * Can be made **HTTP-only** (not accessible to JavaScript).
     * Vulnerable to **CSRF** attacks.
   * **Browser Local Storage**:
     * Accessible to JavaScript but vulnerable to **XSS**.
     * **Should NOT** be used for storing tokens.

### 📱 Single Page Application (SPA)
   * No **secure** place for storing tokens.
   * **Local storage** is unsafe.
   * Authenticate using **username/password** and store tokens **temporarily** in memory.

### 📲 Mobile Application
   * **iOS** can use **Keychain**, and **Android** can use **Keystore** for secure token storage.

---

## 🔐 Securing Data at Rest

### 🔏 Hashed Passwords
   * **Protects user passwords** from being leaked in plaintext form.

### 💽 Transparent Data Encryption (TDE)
   * Encrypts data **on the hard drive**.
   * **Backups are protected**.
   * Data can still be viewed through **queries**.

### 🔐 Client Data Encryption
   * Adds an extra **layer of security**.
   * **Data cannot be viewed** through queries.
   * Queries **cannot** be used to filter or directly update encrypted data.

---

**⚠️ Important Considerations**:
1. Always secure sensitive data with **TLS** during transmission.
2. Be cautious about storing tokens in client-side storage, as **XSS** and **CSRF** vulnerabilities can expose your tokens.
3. Use **refresh tokens** wisely to maintain session security.

 
