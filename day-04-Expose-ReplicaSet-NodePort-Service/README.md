<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 04 Expose ReplicaSet Using NodePort Service.</h1>


<br>

## :dart: About ##

## :sparkles: Features ##

:heavy_check_mark: What is NodePort?;\
:heavy_check_mark: Expose ReplicaSet Using NodePort.;\
:heavy_check_mark: Delete ReplicaSet and NodePort Service.;
## :rocket: Technologies ##

The following tools were used in this project:
- [Previous Blogs](https://m3pratik.hashnode.dev/)
- [GitHub](https://github.com/m3pratik/31daysofEKS)
- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

## (1) What is Services in Kubernetes?
 
  There are 4 Types of services.
  1. ClusterIP
  2. NodePort
  3. Load Balancer
  4. External Name
 
 Kubernetes ServiceTypes allow you to specify what kind of Service you want.
 
 It allow us to communicate with running pod on a Port of the Node.

 ### NodePort: Exposes the Service on each Node's IP at a static port (the NodePort). To make the node port available.

 - Reference: https://kubernetes.io/docs/concepts/services-networking/service/

## (2) Creating ReplicaSet.

- Create ReplicaSet
```
kubectl create -f frontend.yaml
```
- **frontend.yaml**
```yml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: guestbook
    tier: frontend
spec:
  # modify replicas according to your case
  replicas: 3
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: php-redis
        image: gcr.io/google_samples/gb-frontend:v3
```
 - **Important Note:** `frontend.yaml` is include in current directory.

### List ReplicaSet
- Get list of Created ReplicaSet
```
kubectl get replicaset
kubectl get rs
```

## Step-03: Expose ReplicaSet
- Expose ReplicaSet using NodePort Service to access the application from browser.
```
# Expose ReplicaSet
kubectl expose rs frontend  --type=NodePort --port=80 --target-port=8080 --name=frontend-service

# Check created Service
kubectl get service
      OR
kubectl get svc

# Get Public IP of Worker Nodes
kubectl get nodes -o wide
```
- **Access it using Public IP**
```
http://<node1-ip>:<NodePortNumber>/index.html
```

## Step-04: Delete ReplicaSet & NodePort
### Delete ReplicaSet
```
# Delete ReplicaSet
kubectl delete rs <front-end

# Verify
kubectl get rs
```

### Delete Service created for ReplicaSet
```
# Delete Service
kubectl delete svc front-end-service

# Verify
kubectl get svc
```
## :memo: License ##

Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
