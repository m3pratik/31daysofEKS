<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 02 Creating first pod in EKS and accessing.</h1>


<br>

## :dart: About ##

## :sparkles: Features ##

:heavy_check_mark: What is a pod?;\
:heavy_check_mark: Creating a first pod.;\
:heavy_check_mark: SSH into created pod.;

## :rocket: Technologies ##

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

## (1) What is pod?
 
 According to official kube-doc: Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
 - Reference: https://kubernetes.io/docs/concepts/workloads/pods/

## (2) Creating first pod
 ### There are two ways to create a pod
  (i) Using Imperative commands
 ```
 kubectl run first-pod --image nginx:1.14.2
 ```
  (ii) Using Declarative .yaml files
 ```
  kubectl apply -f simple-pod.yaml
 ```
 - **Important Note:** `simple-pod.yaml` is include in current directory.


## (3) Describing created pod and SSH into it.

### Showing running Pods
```
kubectl get pods
```

### Describing pod
```
kubectl describe pod nginx
```

### Get a Shell to a Running Container.

```
kubectl exec --stdin --tty nginx -- /bin/bash
```

## :memo: License ##

Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
