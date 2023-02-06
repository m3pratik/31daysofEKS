<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 17 NameSpace | Kubernetes.</h1>


<br>

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

### what is namespace?

* Namespaces are also called `virtual clusters` in our physical Kubernetes cluster.
    
* We should use `Namespaces` where we have many users spread across multiple teams over projects.
    
* Namespace creates `isolation boundary` from other Kubernetes objects, also we can limit the resources like `CPU, Memory` on per namespace basis(Resouce Quota)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675419539339/6f98c7f2-7332-4aab-9329-98607d149deb.png align="center")

`Kubelet` having some default namespaces that used by kubernetes to manage the operations. like `default` , `kube-*` etc.

### How to create NameSpace?

There are two ways to create the namespaces.

1. Using `kubectl` command.
    
    `kubectl create namespace dev3`
    
2. Using Declarative `yml` file.
    
    %[https://gist.github.com/m3pratik/c7891b1d2a7c4bbe50d367339efcafec] 
    

**Namespaces** provide a way to logically separate resources within a single cluster and enable better resource management. For example, if you have multiple teams working on different projects in the same cluster, you can create different namespaces for each project.

**Names** of resources must be unique within a `namespace`, but not across namespaces. This means that you can have two resources with the same name in different namespaces. This is especially useful when you want to reuse the same resource name across multiple projects.

* Reference: [https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)
    
* Reference: [**github.com/m3pratik/31daysofEKS**](http://github.com/m3pratik/31daysofEKS)
    

Made with ❤️ by [**Pratikkumar Panchal**](https://www.linkedin.com/in/m3pratik/). [**github.com/m3pratik/31daysofEKS**](http://github.com/m3pratik/31daysofEKS)

<a href="#top">Back to top</a>
