<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 16 Readiness Probe Kubernetes.</h1>


<br>

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

Yesterday in this blog [https://m3pratik.hashnode.dev/day-15-liveness-probe-kubernetes](https://m3pratik.hashnode.dev/day-15-liveness-probe-kubernetes) we talk about types of `probes`, in that blog, we learn how to use liveness probes to make applications up all the time.

In today's blog, we will learn about `Readiness Probe`!

### What is the readiness probe?

The `kubelet` is an important part of a Kubernetes cluster, as it is responsible for managing the pods, containers, and other resources. It ensures that containers are running, healthy, and ready to accept traffic. This is done by using readiness probes.

A readiness probe is a signal used to detect when a container is ready to start accepting traffic. The `kubelet` uses this signal to determine which pods are ready to be used as backends for services. If a pod is not ready, then it is removed from the service load balancers. This is important because it prevents traffic from being routed to a pod that is not ready to handle it.

### How to use the readiness probe?

```yaml
          readinessProbe:
            httpGet:
              path: /login #this path can be different.
              port: 3000
            initialDelaySeconds: 60
            periodSeconds: 10  
```

%[https://gist.github.com/m3pratik/95bbfb154cc72ea338bb2b601ac58195] 

In the above readiness probe, we use `path` : /login and method `httpGet` so that it can send get request to the current pod's endpoint and check the status, if response is not 200 it will show as `not ready` state and the container will restart.

* Reference: [**https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/**](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)
    
* Reference: [**https://github.com/m3pratik/31daysofEKS/**](https://github.com/m3pratik/31daysofEKS/)
    

Made with ❤️ by [**Pratikkumar Panchal**](https://www.linkedin.com/in/m3pratik/). [**github.com/m3pratik/31daysofEKS**](http://github.com/m3pratik/31daysofEKS)
&#xa0;

<a href="#top">Back to top</a>
