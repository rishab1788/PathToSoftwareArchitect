What is kubernates ? 
- Kubernates is a portabnle extensible open source platefrom for managine containerzed workload and service that failcitya both declartive confiureation and autoantion it has large raipd grouwing ecodsystem.

- - a contianer platform
  - a microservices platform
  - a portable cloud platform and a lot more
  - 
Note : support Docekr contianerD CRIO

BAE Kubernates Architecture 

<img width="470" alt="image" src="https://github.com/user-attachments/assets/4c486155-455d-405e-a52b-11d68655712b" />

Base Kubernates
<img width="473" alt="image" src="https://github.com/user-attachments/assets/ae3f3228-3c10-4778-b549-28e991122420" />


Kuberante Architecture - COntroller Manager 

A controller is a loop that drives the control towards the desired state-communicates with API server to create, update and delete the reosujfce it manges.
-Runs the controller 
  - Node COntroller - noticing and responding when nodes go down
  - Replication conrtoller - maintans correct offer of pods for every replication controlle object in the system.
  - Endpoints COntroller - Popuklates endpoints -jons services & pods service accoutn & token Conmtroller cread defuaklt accoutn & API tokens for name spaces.
  - Cloud-controller-manager - Controller that interacts with underlying lcoud providers (node status, routes, cloud Ib and volumens)



Kubernates Architecture- Scheduler 

- Wathced for newly created pods that have no node assigened and selects the node for them to run on
- take into account
- resource reqruiedments (Collective)
- hardware/software/policy constraints
- Anti affiently specs.
- Data Localtiy.



Kuberantes Architecture - Kubelet 
- Atgent that runs on each node
- Takes care of starting, stopping and maintian container
- Sends node status to cotnroelr plane via a heartbeat
- Takes a set of podspecs trhough vvariours method and confirms containerr in that spec are running & healthy
- Kubelt ignortes cotnaienr not creatd by k8S.


Kuberantes Architecture - Kube-proxy 
  _ network proxy and load balaner that runs on each node.
  - suport service abstraction with other netweroking operation
  - maintains networking rules
  - perform connection forwarding

API Server ------------> [Kubeproxy] -> IP tables.


Kuberantes ARchitecture - POD 
- GROup of one or more contaienr with shared storage/network tightly coupled
- Pods contents are alwawys colocated & schdeuled together -- run in shared context...
- DOcker Model - pods is group of container in shared namespace & sahred volumnes.
- Ephemeral - like all container


Kuberante Architecture - Network Plugin (CNI)
 - Controle how pods will communicates to each otehr across nodes
 - Creates a clean & compatible model where pods are treaed much like Vms
 - Fundamental Reqruiemetns
 - All container can communicate with all other cotnaienr without NAT
 - All nodes can cmmunication with all cotnaienr vice-versa without NAT
 - The IP the cotaniers sees itself as is the same IP that othere octnaienr see it as.

OPtions - CISCO ACI, BIG CLUOUD , KUUBER ROUTER, NSX-T\

<img width="551" alt="image" src="https://github.com/user-attachments/assets/bb9bab7a-e1db-4503-bcb4-d99ba6c32541" />

Priamry is already managed, NODES are not managed so can tweak there.


Deployment Types -

1. General POD Deployment
   - Only runs the pod and will not restart if deleted. ( good for creating Tools)
2. Replica Set
   - Next gernation replica controller
   - Ensure that the desired number of pods (Replicas are running )
   - <img width="1312" alt="image" src="https://github.com/user-attachments/assets/f88577ad-b3a3-4361-9d2b-34093d4e8621" />

3. StatefulSet
   - Manages deployment & scaling of pods.
   - Provides gurantees about ordering & uniquness.
   - Maintains strict identify of the pod (Persistend identifiers) (is not designed )
   - <img width="1152" alt="image" src="https://github.com/user-attachments/assets/2e7217ce-e83c-48f4-b467-aea5ea5670d0" />

4. Deployment
   - Descirber desired state of a replicaSet
   - Deployment controller chjanges the actual state of desired state at a controller rate
   - Can create new replicasets or adopt existing deployment resources.
<img width="1332" alt="image" src="https://github.com/user-attachments/assets/a92793c8-54b3-4049-82ed-c8ac8446487f" />

<img width="1357" alt="image" src="https://github.com/user-attachments/assets/7358f3eb-f6fc-48e3-a134-2d58f3b3c028" />



Services & Ingress 
- Services
  - Services defuines a logical set of pods
  - Defines an access policy.
- Ingress Controller
  - API object that manges external access.
  - Ingress can provide load balancing SSL.
  - Termination or name based hosting
 
  - <img width="1230" alt="image" src="https://github.com/user-attachments/assets/a6cfbc7f-899e-4027-9683-1e8ca7d34f4d" />

<img width="1374" alt="image" src="https://github.com/user-attachments/assets/544473cc-1ad0-4be0-af47-a82cdae01fd9" />

<img width="1344" alt="image" src="https://github.com/user-attachments/assets/79cabfee-535f-4fdb-a822-127b7f79bc66" />

Running a cluster 

Cloud - 
  EKS - Managed AWS kubernates - unmanages nodes, managesd nodes and fargate profiles 
  AKS - manages azure 
  GKE - 
Local --
  - Docker Desktop
  - - Minikube
    - K3s


  Running a cluster - Docker Desktop 
    Install Docker Desktop 
    Enable Kubernates support under System prefrences

Interacting with a cluster - 
KubeCtl - CLI tghat lets you interact with clusters 

- Looks at $Home/.kube/config, KUBECONFIG environment variable or --kube

Genral commnads -
<img width="645" alt="image" src="https://github.com/user-attachments/assets/b49c8635-89c9-4229-aba3-34fe4e9d3152" />


<img width="922" alt="image" src="https://github.com/user-attachments/assets/8f00e9fd-71a0-48bc-a528-13cdb3ca4448" />


<img width="352" alt="image" src="https://github.com/user-attachments/assets/30bf160d-f547-4ade-ab53-726789e3ae85" />



Services - 

K8s Service allows us to expose a pod oir set of pods as a single endpoint 
BNoth a Rest oobject and an abstraction that defines: 
  - Set of pods
  - Policy to access them.
Services keep tracks of the changes in IP address and DNS names - expose as a single object.
- Different types of backends:
  Native K8s applications - endpoint API is udpated wherener thre are hcanges - uses selector
  Non-native K8s application -virtual IP bridge or load balcner to direct traffice to baceknd.

4 types of services - 
  Cluster IP /Headless
  NodePort
  Load balancer
  External Name

Selector - App - AAPA
Services : 

1. Cluster IP 
- Defauilt service type with an IP that things access
- Load Balances between backend services

2. Headless 
- Used when load balancing and service IP are not required
- Creates list of A records - kube-proxyu will ignore them

3. NodePort 
- Exposes the service on an IP of the node with a static port
- Cluster IP is created to help with routing
- Connect at <NodeIP>:<NodePort>

4. Load Balancer -
 _ Exposing cluster to the internet
 - Will create A LB in AWS.

 5. External name
      - Lets you map external services to k8S service name

DNS in Kubernates 
  Kubernates DNS  < 1.11 kube dns , > 1.11 coredns 
  Both implementaiton work in simmilar matter 
  - Service named kube-dns w/one or more pods.
  - Kube-dns serivce listen for service and endpoint events from k8s API and then records.
  - Kubelet sets /etc/resolv.conf nameserver, search and options setting
  An a record of a kubernatesd service looks like -
    server.namesspace.svc.cluster.local

Kube-dns 
 - 3 contianrs in a pod.
 - KubeDNS - skydns contianer that perform DNS resoluition
 - DnsMasq - cahce 
 - Sidecar - handle metrics

DNS In kubernates 

<img width="641" alt="image" src="https://github.com/user-attachments/assets/bc0b6038-0ae7-4f3c-83f6-f096877afc6d" />


Readiness & Liveness Check 
- Liveness : probes that determines if your  app is dead or alive - if dead k8s removes the starts a replacement
- Readiness - Probles desinge to deremine if your application to service traffice - allow service to send traffic
- Actions are performed by kubelet.
- Probes:
  - HTTP
  - Command
  - TCP

1. Liveness Probe
Checks if a container is still running and responsive.
If the liveness probe fails, Kubernetes kills and restarts the container.
Useful for detecting stuck or unresponsive applications.
Example: Liveness Probe
Here, the probe checks if the application responds on port 8080. If it fails, Kubernetes restarts the container.

yaml
Copy
Edit
livenessProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 3  # Wait before first check
  periodSeconds: 5        # Check every 5 seconds
  failureThreshold: 3     # Restart container after 3 failures
Use Case:

A web server stuck in an infinite loop can be detected and restarted.


Readiness Probe
Checks if a container is ready to accept traffic.
If it fails, the pod is removed from service endpoints until it recovers.
Prevents sending traffic to an unready application.
Example: Readiness Probe
Here, the probe ensures the app is ready to handle traffic before adding it to the load balancer.

yaml
Copy
Edit
readinessProbe:
  httpGet:
    path: /ready
    port: 8080
  initialDelaySeconds: 5  # Wait before first check
  periodSeconds: 10       # Check every 10 seconds
Use Case:

A database-dependent service should not receive traffic until it successfully connects to the database.

Service Discovery -
 Leverages service model in combination with readiness/liveness checks 
 Server-side discovery
   - Simmilar to traditional load balancer - AWS NLB
   - Levragfe clusterIP and K8S Balances
Service-side discvery
  Headlerss services - application makes choice
Need to decide on best model for your service
  - keep in mid K8s Load Balancer arennt very smart - round robin

 
