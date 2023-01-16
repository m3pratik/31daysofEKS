<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 09 Storage in Kubernetes.</h1>


<br>

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

### Introduction:

Containers/Pods are ephemeral so On-disk files too. it creates many problems for non-trivial applications running in containers. One of the biggest problems is the loss of files when a container crashes. The `Kubelet` service will restart the container but with a clean state.

To overcome this, we have `volumes` in Kubernetes that helps us persist data, no matter what happens with pods/containers we always have data available when needed.

### Storage Classes

A StorageClass provides a way for administrators to describe the "classes" of storage they offer. Different classes might map to quality-of-service levels, or to backup policies, or to arbitrary policies determined by the cluster administrators. Kubernetes itself is unopinionated about what classes represent. This concept is sometimes called "profiles" in other storage systems.

* Reference: [https://kubernetes.io/docs/concepts/storage/storage-classes/](https://kubernetes.io/docs/concepts/storage/storage-classes/)
    

Each StorageClass contains the fields `provisioner`, `parameters`, and `reclaimPolicy`, which are used when a PersistentVolume belonging to the class needs to be dynamically provisioned.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1673867974982/154be32c-831e-4602-bca6-9fd3e9bb7d82.png align="center")

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
reclaimPolicy: Retain
allowVolumeExpansion: true
mountOptions:
  - debug
volumeBindingMode: Immediate
```

### *PersistentVolume* (PV)

A *PersistentVolume* (PV) is a resource in the cluster just like a node is a cluster resource.

PVs are volume plugins like Volumes, but have a lifecycle independent of any **individual Pod** that uses the PV.

### *PersistentVolumeClaim* (PVC)

A *PersistentVolumeClaim* (PVC) is a request for storage by a user/pod/container. It is similar to a Pod.

Pods consume `node resources` and PVCs consume `PV resources`. Pods can request specific levels of resources (CPU and Memory). Claims can request specific size and access modes (e.g., they can be mounted ReadWriteOnce, ReadOnlyMany or ReadWriteMany, see [AccessModes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes)).

**Persistent Volume Life Cycle**

1. Provisioning
    
    * Static
        
    * Dynamic
        
2. Binding
    
3. Using
    
4. Reclaiming
    

Storage is indeed one of the crucial part of kubernetes lifecycle. In upcoming blog will cover how effectively we can use `PVC` and `PV`, with some real usecases.


Made with :heart: by <a href="https://www.linkedin.com/in/m3pratik/" target="_blank">Pratikkumar Panchal</a>

&#xa0;

<a href="#top">Back to top</a>
