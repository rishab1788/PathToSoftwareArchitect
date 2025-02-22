apiVersion: v1 
kind: 
metadata: 
  name: myapp-pod
  labels:
    key
spec:
  
apiVersion:version of k8s version
kind: k8s objects
metadata: define name and labels for k8s objects
spec: specification or real definition foir k8s objects

-----
apiVersion: v1 
kind: Pod
metadata:  #disctionary
  name: myapp-pod
  labels:
    app: myapp
    tier: frontend
spec:
  containers: #List
    - name: myapp
      image: stacksimplfy/lube:1.2.2
      ports: 
        - containerPort : 80
    - name: myapp-backend
      image: stacksimplfy/lube:1.2.2

Create nodeport service -

apiversion: v1
kind:Service
metadata:
  name: myapp-pod-nodeport-service
  labels: 
    app: myapp
spec: 
  type: NodePort #load balancer, 
  selector:
    app: myapp
  ports: 
    - name: http
      port: 80 # Service pOrt
      targetPort: 80 #container Port
      nodePort: 31231 D#nodeport
  

##########################


K8s ConfigMaps and Secrets - 

ConfigMaps -
- API object to start non-confidential data in k/v pairs
- Can be consumed in the following ways:
  - Enviorment Variblae
  - CLI Arguments (uses envior varibnlae)
  - Volumes
  - K8S Integraion w/RBAC
- Data can be the follwing
  - Data: UTF-8 string
  - binaryData: base64-encoded strings

Secrets 
- API object that contains sensitive data
- Can be consumner in the following ways
  -   File in a volumes
  -   Enviorment Variable
  -   Kubelt when pulling images
- Multiple types
  - OPauq - arbitraty user defined data
  - K8s geneerated Service token
  - serialized
  - basic auth

Secretes - Secutiry 
- configmaps and secrets work in simmilar ways but secrets have extra protections.
- Only sent to the node the pod lives on-bot all nodes
- if multiple containers are in pod- the one where the secret is mapped to is the only one that can see it.
###############


Assigning pods to nodes 
node selctors 
 - Simplest form for node selections
 - Add nodeSelector field to POD specification
 - K8s will only scheudel on nodes that have that corresponding conditions
Node isolation/restrictions
- a set of labels that the kublet cont modify - prevents comprimised nodes from setting the lavel.

Deployment Stratgeies - ROlling 
 - Standard deployment  method
 - Slowley deployes one by one
 Blue/Green -
  Not a specific part of deployment spec.
A scenonday deployment is created (Green)

canary & A/b
- This reqruied service mesh based tooling to happen - Isti, consul;, envou or ingress objects 
- 
