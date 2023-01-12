<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 08 Pause and Resume Deployment in Kubernetes.</h1>


<br>

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

### Introduction:

Previously we did deployments with various container images, Rollback in Kubernetes is a life server in case of reverting the deployed code.

Rollback can be done for either `previous` or `specific` the version of **deployment**.

### (1) Introduction:

Now you are going to get to know why you will have to pause the deployment of your code.

For instance, you have multiple `micro-services` deployed in the Kubernetes cluster, and you would like to do multiple changes on it and wish to deploy in one go. Use pause deployment so that you can make several changes on eighter `application image` or `Kube-configs` , it will be in the queue until Resume.

### (2) Pausing Deployment

```bash
# Pause the Deployment
kubectl rollout pause deployment/nginx-deployment

# Update deployment image 
kubectl set image deployment/nginx-deployment nginx=nginx:1.2.1 --record=true

# Check the Rollout status
kubectl rollout history deployment/nginx-deployment  
# Note: Previously when we have updates made to our deployment process it would automatically start rolling out but this time due to a paused deployment, there won't be any new changes shown.

# Lets make one more change
kubectl set resources deployment/nginx-deployment  -c=nginx --limits=memory=50Mi
```

### (3) Resume Deployment

```bash
# Resume the Deployment
kubectl rollout resume deployment/nginx-deployment

# Check the Rollout History of a Deployment
kubectl rollout history deployment/nginx-deployment  
# Note: Have you notices a new version got created

# Get list of ReplicaSets
kubectl get rs
# You can see the new replicaSet being created.
```

I hope you understand how these Kubernetes features are working. This is also play major part on ci-cd deployment process. In future blog will see more usage of rollout operator.  
  
Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
