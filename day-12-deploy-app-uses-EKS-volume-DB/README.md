<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 12 Deploy App use EKS Volume-based DB.</h1>


<br>

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

Yesterday We have created PostgreSQL DB backed by EKS CSI Based EBS volume. Today We are going to use that DB with the newly deployed application.

For this LAB Demo, I am using below application:

* Reference: [https://github.com/JamesHuangUC/Ruby-on-Rails-CRUD](https://github.com/JamesHuangUC/Ruby-on-Rails-CRUD)
    

### (1) Create a Deployment.

```yaml
apiVersion: apps/v1
kind: Deployment 
metadata:
  name: rails-crud-microservice
  labels:
    app: rails-crud
spec:
  replicas: 1
  selector:
    matchLabels:
      app: rails-crud
  template:  
    metadata:
      labels: 
        app: rails-crud
    spec:
      containers:
        - name: rails-crud
          image: 943874580445.dkr.ecr.us-east-1.amazonaws.com/crud:v2 # replace this image with your uploaded Image
          ports: 
            - containerPort: 3000           
          env:
            - name: POSTGRES_HOST   # this type of env declaration is not recommanded for production usecase
              value: "postgres"                       
            - name: POSTGRES_USER
              value: "postgres"            
            - name: POSTGRES_PASSWORD
              value: "postgres123"
```

### (2) Create NodePort Application Service.

To access the application from the browser, we use the NodePort service here.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: rails-crud-service
  labels: 
    app: rails-crud
spec:
  type: NodePort
  selector:
    app: rails-crud
  ports: 
    - port: 3000
      targetPort: 3000
      nodePort: 31231
```

### (3) Apply the Kubernetes manifest.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674040003960/97b4c770-a82a-412d-a57a-4d5e65e58585.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674040020421/658a7468-668a-425a-888a-9378179c43e2.png align="center")

Now Open the browser, with worker-node-ip and nodeport port. like  
`http://<WorkerNode-Public-IP>:31231`

You can see the application is live... you can delete the `pod` and see the magic.


Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
