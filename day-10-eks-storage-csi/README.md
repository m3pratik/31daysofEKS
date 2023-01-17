<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 10 AWS EKS Storage | Container Storage Interface (CSI).</h1>


<br>

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

In a previous blog, we saw, the importance of persistence storage. AWS Provides EBS Volumes that help us achieve the same. Let's talk more about EBS.

* EBS provides `block-level storage volumes` for use with EC2 & Containers.
    
* These are the portable volumes, that we can directly mount `volumes` as devices in our `EC2` or `container instance` .
    
* These volumes are independent of `EC2 or Containers` life cycles. i.e if `EC2` or `container` crashes. we have stored data available in `volume` .
    
* Another good thing about EBS volume is we can increase or decrease its configuration dynamically.
    

### Installing EBS CSI Driver

CSI Driver provides a way for the Kubernetes cluster to access the EBS volume. For that, We have to install the CSI driver to our `cluster`.

Firstly, we have to create IAM policy for EBS.

### (1) Create IAM policy for EBS.

* Go to IAM dashboard, Click on create policy and select `JSON` tab.
    

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:AttachVolume",
        "ec2:CreateSnapshot",
        "ec2:CreateTags",
        "ec2:CreateVolume",
        "ec2:DeleteSnapshot",
        "ec2:DeleteTags",
        "ec2:DeleteVolume",
        "ec2:DescribeInstances",
        "ec2:DescribeSnapshots",
        "ec2:DescribeTags",
        "ec2:DescribeVolumes",
        "ec2:DetachVolume"
      ],
      "Resource": "*"
    }
  ]
}
```

`Name` : EBS\_CSI\_Driver\_for\_EKS

* Click on **Create Policy.**
    

### (2) Associate created the policy for Worker Node's IAM Role.

* You can find associated IAM role either from EKS Dashboard or using the command line `kubectl -n kube-system describe configmap aws-auth`
    
* Go to IAM -&gt; Role -&gt; select role with `worker node IAM role name` . -&gt; Click on attach policy and attach the policy name `EBS_CSI_Driver_for_EKS` .
    

### (3) Deploy EBS CSI Driver.

```bash
kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=master"

# Verify csi pods created
kubectl get pods -n kube-system
```

In upcoming blog will make use of these created EBS volumes.



Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
