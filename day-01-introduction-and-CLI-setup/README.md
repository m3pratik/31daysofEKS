<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 01 Introduction</h1>


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

## Install AWS CLI
- Reference-1: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html
- Reference-2: https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
- Validate CLI installation.
```
aws --version
aws-cli/1.23.8 Python/3.9.10 Darwin/22.1.0 botocore/1.25.8

which aws
```
### Configure AWS Command Line using Security Credentials
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
## Step-02: Install kubectl CLI
- Reference: https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html
- Verify the kubectl client version
```
kubectl version --client
```
## Step-03: Install eksctl CLI
## References:
- https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html
- https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html

# Verify eksctl version
```eksctl version```

## :memo: License ##

Made with :heart: by <a href="https://github.com/m3pratik" target="_blank">{{Pratikkumar Panchal}}</a>

&#xa0;

<a href="#top">Back to top</a>
