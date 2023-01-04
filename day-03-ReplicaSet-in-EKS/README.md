<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 03 ReplicaSet in EKS.</h1>


<br>

## :dart: About ##

## :sparkles: Features ##

:heavy_check_mark: What is ReplicaSets?;\
:heavy_check_mark: Creating Replicasets.;\
:heavy_check_mark: Test High availability of ReplicaSets.;
:heavy_check_mark: Scalability in ReplicasSets.;
## :rocket: Technologies ##

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

## (1) What is ReplicaSet?
 
 A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.

 - Reference: https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/

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

## (3) Test High availability of ReplicaSet.
- The main feature of ReplicaSet is to maintain a stable set of replica Pods running at any given time.
- It means if you define there should be atleast `3` pods should be running at anypoint of time, Incase of failure or error any pod(s) crash or fail to load. ReplicaSet will create new pod(s) and maintain the provided number `3` of running pods.

```
# Number of running pods
kubectl get pod

# Delete any running pod.
kubectl delete pod <pod-name>

# Check the numbers of pods running, you will find a newly created pod.
kubectl get pod
```
## (4) Scalability in ReplicasSets.
- In `frontend.yaml` file, key :`replicas` is indicate number of pods.Currently it sets as `3` you can change it to `5`.

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
kubectl apply -f frontend.yaml

# To check newly created pods.
kubectl get pods
```
## :memo: License ##

Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
