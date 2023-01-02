<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 01 CLI setup and Creating first EKS Cluster.</h1>


<br>

## :dart: About ##

Introduction to EKS, and Configurations.

## :sparkles: Features ##

:heavy_check_mark: Installing CLI and connect with AWS;\
:heavy_check_mark: Creating EKS Cluster and Node Groups;\
:heavy_check_mark: Deleting Cluster and Node Groups;

## :rocket: Technologies ##

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting :checkered_flag:, you need to have an Active AWS Account and Basic understaing of Kubernetes concepts.

## :checkered_flag: Starting ##

# Part-1
## (1) Install AWS CLI
- Reference-1: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html
- Reference-2: https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
- Validate CLI installation.
```
aws --version
aws-cli/1.23.8 Python/3.9.10 Darwin/22.1.0 botocore/1.25.8

which aws
```
## (2) Configure AWS Command Line using Security Credentials
- Login into AWS account
- Serch for --> IAM in search bar.
- Select the IAM User, Or create new one. Please make sure you never use Root user's Security credential(Not recommended)
- Click on **Security credentials** tab
- Click on **Create access key**
- Copy Access ID and Secret access key
- Go to command line and provide the required details
```
aws configure
AWS Access Key ID [None]: paste your's
AWS Secret Access Key [None]: paste your's
Default region name [None]: ap-south-1
Default output format [None]: json
```
- Test if AWS CLI is working after configuring the above
```
aws s3 ls
```
## (3) Install kubectl CLI
- Reference: https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html
- Verify the kubectl client version
```
kubectl version --client
```
## (4) Install eksctl CLI
## References:
- https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html
- https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html

## (5) Verify eksctl version
```
eksctl version
```

------
# Part-2

## (1) Create EKS Cluster using eksctl
- It will take few minutes to create the Cluster Control Plane 
```
# Create Cluster
eksctl create cluster --name=demoeks \
                      --region=ap-south-1 \
                      --zones=ap-south-1a,ap-south-1b \
                      --without-nodegroup 

# verify clusters
eksctl get cluster                  
```

## (2) Creating OpenID Connect (OIDC) identity providers.
### References:
- https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_oidc.html
```
eksctl utils associate-iam-oidc-provider \
    --region ap-south-1 \
    --cluster demoeks \
    --approve
```

## (3) Create Public Node Group
```
eksctl create nodegroup --cluster=demoeks \
                        --region=ap-south-1 \
                        --name=demoeks-ng- \
                        --node-type=t3.medium \
                        --nodes=2 \
                        --nodes-min=2 \
                        --nodes-max=4 \
                        --node-volume-size=30 \
                        --managed \
                        --asg-access \
                        --external-dns-access \
                        --full-ecr-access \
                        --appmesh-access \
                        --alb-ingress-access 
```

## (4) Verify Cluster & Nodes
```
# List Nodes in current kubernetes cluster
kubectl get nodes -o wide

# Our kubectl context should be automatically changed to new cluster
kubectl config view --minify
```

------
# Part-3

## Deleting Cluster & Node Groups

### Delete Node Group
- We can delete a nodegroup separately using below `eksctl delete nodegroup`
```
# List EKS Clusters
eksctl get clusters

# List Node Group
eksctl get nodegroup --cluster=demoeks

# Delete Node Group
eksctl delete nodegroup --cluster=eksdemo1 --name=demoeks-ng-1
```

### Delete Cluster  
- We can delete cluster using `eksctl delete cluster`
```
# Delete Cluster
eksctl delete cluster demoeks
```

## :memo: License ##

Made with :heart: by <a href="https://github.com/m3pratik" target="_blank">{{Pratikkumar Panchal}}</a>

&#xa0;

<a href="#top">Back to top</a>
