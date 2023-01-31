<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 15 Liveness Probe Kubernetes.</h1>


<br>

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

Hello again, this time we take a look at various `probe` provided by Kubernetes.

### What is Liveness Probe?

The Liveness probe lets Kubernetes know when to `restart` a container.

There are many cases where the container having issues and the container is running but not serving the needs due to deadlock or any other problem like DB connection failure. restarting a container helps in such states.

### Ways to define probes!

| 1\. Check using Commands | `/bin/sh -c nc -z localhost 3000` |
| --- | --- |
| **2\. Check using HTTP Get Request** | `httpget path:/health-status` |
| **3\. Check using TCP** | `tcpSocket Port:3000` |

```yaml
          livenessProbe:
            exec:
              command:
                - /bin/sh
                - -c
                - nc -z localhost 3000
            initialDelaySeconds: 60
            periodSeconds: 10
```

%[https://gist.github.com/m3pratik/0f148b9163194e6689cdeafd5cdefe24] 

In the above deployment, we defined `liveness` prob, it will exec the command to check the status of that service.

* Reference: [https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)
    
* Reference: [https://github.com/m3pratik/31daysofEKS/](https://github.com/m3pratik/31daysofEKS/tree/main/day-13-kubenetes-secret)
    

Made with ❤️ by [**Pratikkumar Panchal**](https://www.linkedin.com/in/m3pratik/). [**https://github.com/m3pratik/31daysofEKS**](https://github.com/m3pratik/31daysofEKS)

&#xa0;

<a href="#top">Back to top</a>
