<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 06 Updating Kubernetes Deployment EKS.</h1>


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

## (1) why we needs to update the Deployment?
 
 - There are mainly two reasons for that,
   1. general upgrade, labels, replicas, metadata etc.
   2. Changing Deployment container image.
 - Reference: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

## (2) previously created Deployment.

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


## (3) Different ways to update the deployment.
- 1. using kubectl set image option.
- 2. updating deployment yaml file and apply.
- 3. using edit deployment.

### (1) Using kubectl set image deployment/deployment-name

```
kubectl set image deployment/nginx-deployment nginx=nginx:1.15.0 --record=true
# Verify Rollout Status 
kubectl rollout status deployment/nginx-deployment
```

### (2) Making change in (*deployment).yaml file.

- you can change metadata in yaml like replicas, image name etc and apply changes by running `kubectl apply -f nginx-deployment.yaml`

### (3) Using edit deployment

```
# get deployment
kubectl get deployment

#edit deployment

kubectl edit deployment/nginx-deployment

# edit open in vi editor you can change value in here and save it.
# Verify the same using `kubectl get pods` command.
```

Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
