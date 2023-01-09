<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 05 Kubernetes Deployment in EKS.</h1>


<br>

## :dart: About ##

## :sparkles: Features ##

:heavy_check_mark: What is Deployment Service?;\
:heavy_check_mark: Creating Deployment.;\
:heavy_check_mark: Scalability in Deployment.;
:heavy_check_mark: Expose Deployment Service.;
## :rocket: Technologies ##

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

## (1) What is Deployment?
 
 A Deployment provides declarative updates for Pods and ReplicaSets.

 - Reference: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

## (2) Creating Deployment.

- Create Deployment
```
kubectl create -f nginx-deployment.yaml
```
- **nginx-deployment.yaml**
```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
 - **Important Note:** `nginx-deployment.yaml` is include in current directory.

### Check Deployments
- Get list of Created ReplicaSet
```
# Verify Deployment
kubectl get deployments
kubectl get deploy 

# Describe Deployment
kubectl describe deployment my-first-deployment

# Verify ReplicaSet
kubectl get rs

# Verify Pod
kubectl get po
```

## (3) Scaling Deployment

```
# Scale Up the Deployment
kubectl scale --replicas=20 deployment/nginx

# Delete a running pod.
kubectl get pods
kubectl delete pod <pod-name>

# verify newly created pod is working.
kubectl get pod
```
## (4) Scaling Deployment with yaml
- In `nginx-deployment.yaml` file, key :`replicas` is indicate number of pods.Currently it sets as `3` you can change it to `5`.

```
# Before
spec:
  replicas: 3

# After
spec:
  replicas: 5
```
- Update the ReplicaSet
```
# Below command will again read the file and change the replicas.
kubectl apply -f nginx-deployment.yaml

# To check newly created pods.
kubectl get pods
```
## (5) Expose Deployment Service
- Exposing deployment allow us to access the service from internet.(NodePort)

```
# Expose Deployment Service
kubectl expose deployment nginx-deployment --type=NodePort --port=80 --target-port=80 --name=nginx-deployment-service

# find nodeport port
kubectl get svc

# Get Public IP of Worker Nodes
kubectl get nodes -o wide
```
 
### Access the Application using Public IP
http://<node-public-ip>:<node-port-port>

## :memo: License ##

Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
