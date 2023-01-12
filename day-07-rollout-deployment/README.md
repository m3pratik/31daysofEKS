<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 07 Rollout Deployment EKS.</h1>


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

### (1) Rollback Deployment to the previous version.

```bash
# we can list deployment versions using below command.
kubectl rollout history deployment/nginx-deployment

# Rollback to previous version
kubectl rollout undo deployment/nginx-deployment

# Verify the rollbacked deployment.
kubectl get deployment
kubectl describe deployment/nginx-deployment
```

* Once you found that the `rollback` is completed you can check with **URL**.
    

### (2) Rollback to a Specific Version.

```bash
# we can list deployment versions using below command.
kubectl rollout history deployment/nginx-deployment

# assign specific version value to --to-revision=#n
kubectl rollout undo deployment/nginx-deployment --to-revision=5
```

### (3) Restart the deployment in a rolling fashion.

In case you have to re-deploy the same deployment you can use this feature.

`kubectl rollout restart deployment/nginx-deployment`  
  
Made with :heart by [**Pratikkumar Panchal**](https://www.linkedin.com/in/m3pratik/)
Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
