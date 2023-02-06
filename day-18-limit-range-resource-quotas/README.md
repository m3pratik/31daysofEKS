<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 18 Resource Quota & Limit Range | Kubernetes.</h1>


<br>

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

As a Kubernetes administrator, you need to ensure that your Kubernetes `cluster` and its associated namespaces are configured to provide fair and equitable access to `compute resources`. This is especially important if you have a large number of users and workloads running on the cluster.

Using Kubernetes `Resource Quotas` and `LimitRanges`, you can ensure that each workload running on the cluster is allocated a fair share of the `cluster resources`.

`Resource Quotas` can be used to limit the amount of CPU and memory resources allocated to a namespace, ensuring that no single namespace consumes more than its fair share. Resource Quotas can also be used to limit the amount of persistent storage within a namespace.

%[https://gist.github.com/m3pratik/6ac6f80a0d5b33117d02fe64c16a91af] 

`LimitRanges` provide a more granular approach to resource allocation within a namespace. They provide the ability to set specific limits for individual objects (such as Pods and PersistentVolumeClaims).

**For example**, you can set a LimitRange within a `namespace` to ensure that no `individual` Pod can consume more than a certain amount of `CPU or memory`. This ensures that no single Pod can monopolize all the available resources within its namespace.

You can also set a LimitRange to ensure that no PersistentVolumeClaim within a namespace can request more than a certain amount of storage. This is useful if you want to ensure that no single namespace user can consume all the available storage resources within a namespace.

%[https://gist.github.com/m3pratik/1fde91c91885737cfcbffd28193a8895] 

Using Kubernetes Resource Quotas and LimitRanges, you can ensure that your Kubernetes cluster is configured to provide fair and equitable access to compute resources. This is especially important if you have a large number of users and workloads running on the cluster.

* Reference: [https://kubernetes.io/docs/concepts/policy/limit-range/](https://kubernetes.io/docs/concepts/policy/limit-range/)
    
* Reference: [**github.com/m3pratik/31daysofEKS**](http://github.com/m3pratik/31daysofEKS)
    

Made with ❤️ by [**Pratikkumar Panchal**](https://www.linkedin.com/in/m3pratik/). [**github.com/m3pratik/31daysofEKS**](http://github.com/m3pratik/31daysofEKS)

<a href="#top">Back to top</a>
