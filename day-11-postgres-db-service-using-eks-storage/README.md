<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 11 Postgres DB Service Using EKS Storage.</h1>


<br>

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

### (1) Introduction:

* We are going to create a Postgres database with persistence storage using AWS EBS Volumes.
    

| Kubernetes Object | YAML File |
| --- | --- |
| Storage Class | 01-storage-class.yml |
| Persistent Volume Claim | 02-pvc.yml |
| Config Map | 03-create-db-configmap.yml |
| Deployment, Environment Variables, Volumes, VolumeMounts | 04-pg-deployment.yml |
| ClusterIP Service | 05-pg-service.yml |

### (2) Create the following Kubernetes manifests.

**(i) Create a Storage Class manifest.**

* Reference: [https://docs.aws.amazon.com/eks/latest/userguide/storage-classes.html](https://docs.aws.amazon.com/eks/latest/userguide/storage-classes.html)
    

**(ii) Create Persistent Volume Claims manifest.**

```bash
# Create Storage Class & PVC
kubectl apply -f kube-configs/

# List Storage Classes
kubectl get sc

# List PVC
kubectl get pvc 

# List PV
kubectl get pv
```

**(iii) Create ConfigMap manifest**

* We are going to create a `railsv1` database during the `postgres` pod creation. we will use it when we deploy Application Microservice.
    

**(iv) Create Postgres Deployment.**

* Environment Variables
    
* Volumes
    
* Volume Mounts
    

**(v) Create Postgres ClusterIP Service manifest.**

* At any point in time, we are going to have only one `postgres` pod in this design so `ClusterIP: None` will use the `Pod IP Address` instead of creating or allocating a separate IP for `Postgres Cluster IP service`.
    

### (3) Create Postgres Database with all the above Kube-configs.

```bash
# Create Postgres Database
kubectl apply -f kube-manifests/

# List Storage Classes
kubectl get sc

# List PVC
kubectl get pvc 

# List PV
kubectl get pv

# List pods
kubectl get pods 

# List pods based on  label name
kubectl get pods -l app=postgres
```

### (4) Connect to Postgres Database.

`kubectl exec -it pod-name -- psql -U postgres`

### (5) Verify 'railsv1' DB is created.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673970450466/69277659-5077-49c2-91ff-0b352795bb20.png align="center")

  
Made with ♥ by [**Pratikkumar Panchal**](https://www.linkedin.com/in/m3pratik/)



Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
