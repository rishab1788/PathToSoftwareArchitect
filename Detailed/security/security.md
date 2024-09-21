
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


Hashing 
            for secure communication we do Hashing

 its a algorithm which convert input to hash output
            
There are different hashing mechanishm available.
Hasing is a one-way algorithm
Generate same output for same text
Slighteest change in the text changes the hash value drastically .
two input can also result in hash but it does not happen now. 


            MD5 - 128 bits
            SHA=1 - 160 bits
            SHA=2 - 256.512 bits
            SHA=3

Digital Signatures - 
are the way to check intergrity and authentication and non-republication of doucment.

we have Data document ---> hash will be generated --> signer will use public key ----> 
Verified using public key of signer. 
Message is hashed independently, and copared with the hash present in the signature.



Digital Certificates - 
            Way of sharing public key with the world. in a trusted manner
            * any client should be able to verify who the public key owner is



Chain of trust - 
            End-entity certificate 
            Owners name
            Owners public key 
            Issurs (CA's)




Secure Network Channel 
            * Certificate & keys deployed on external load balncer.
            So we have learned that we can use TLS communication

            over the internet, and that's the right thing to do
            because once communication is happening over the internet
            anyone who has the access to the internet,
            which pretty much anyone can have,
            can not only view the data, but more importantly
            can make sense out of it if we are not using TLS.
            But if we are using TLS,
            then only the data can be viewed in the encrypted form
            but nobody can make sense out of that.

            Firewalls - external infrastructure to allow and deny.
            They are fitler they look for are the request comming from client are allowed or not.
            Firewall has two functions 
            1. Ingress
                        * source IP (Range)
                        * Target IP (Range)
                        * Target port 
                        * protocol -> TCP, UDP
            2. Egress 
                        * Destination IP (Range)
                        * Target IP (Range)
                        * Target Port 
                        * Protocol 

Network Security 
            4 subnets -
            [DMZ - Subnet 1 ]  [DMZ Subnet 2 ]     [Services Subnet]   [DB Subnet]

             port 443       port443 for internal host
           {Webapplication}  [aggregator service]   8080(port)         Port 1522

Identity Management 
   Authentication/ Authorization 

   * Authentication (who you are)
      * Proving an Identity
         - ID
         - Name
         - Organization
   * Authorization (what you can do)
    -  Proving right to acces s function/services
    -  Data


     Creds trasnfer
     [Chrome]-------------> [Auth Service] ---------------> [LDAP/RDBMS]

Credntials Transfer 
            HTML Forms
                        * HTTP post method over SSL/TLS
            HTTP Basic 
                        * Based on Chanllange-Response
                        * HTTP methdhos overs SSL/TLS
                        * Base 64 encoded <UserId> <Passwords>
            Digest Based 
                        * like basic but uses hashed password
                        * Hash = md5 (username:realm:password)
            Certificate based 
                        * private-public keybased certificates exchanges.

        Credential Storage & Verfication 
                     Two things two store -
                        User Auth -> ID, Name, Role , Group 
                        User info -> Org, Address, Contact.
                        
         File Storage 
            * Not scalable 
         Datebase 
            * RDBMS 
            * NoSql 
         LDAP/Directory Server (Lightweight Directory Access Protocol))
                     https://www.youtube.com/watch?v=Xp9kLn9vRmw
            * Architectural 
              * Hierachical database desinged for reading browsing, searching data.
              * High scalablity and high performance for read loads.
            * Enviorment 
              * Enterprice enviorment with multiple application.
              * Interoperability with all LDAP clients.
              * Distributed/Fedration Storage.
              
Stateful Authentication 
            * Limited Scalability due to sessions and centralized authentication 
            * Sessions can be revoked by removing it from session storage.
             we will use common cache to store session values. 
