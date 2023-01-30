<div align="center" id="top"> 
  <img src="./.github/app.gif" alt="Day 01 Introduction" />

  &#xa0;

</div>

<h1 align="center">Day 14 init container Kubernetes.</h1>


<br>

The following tools were used in this project:

- [AWS CLI](https://aws.amazon.com/cli/)
- [kubectl - Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/)
- [eksctl - CLI for Amazon EKS ](https://eksctl.io/)
## :white_check_mark: Requirements ##

Before starting this hands-on make sure your cluster is up and running with node groups.

## :checkered_flag: Starting ##

As word `init` describe, `init containers` are run **before** application containers run.

In some scenarios, we have to `verify` or `perform certain action` before starting the app container, like installing `utilities` or `run a setup script` etc. at that time, we can leverage the `init container`.

Some facts about `init containers`.

* We can run **multiple** init containers before the app container.
    
* init containers always run to `completion`.
    
* Each init contianer must `complete successfully` before the next one starts.
    

Let's do some hands-on with the init container.

In previous labs, we have created `ruby on rails crud app` , we are going to add an init container in that same config,

```yaml
 initContainers:
        - name: init-db
          image: busybox:1.31
          command: ['sh', '-c', 'while ! nc -z postgres 5432; do sleep 1; printf "-"; done; echo -e "  >> Postgres DB Server has started";']
```

%[https://gist.github.com/m3pratik/64651bd8c764d409f60a83066064ba41] 

What if the application started serving the request and `database` service is not up and running? `nightmare` right?

to overcome this, we can use the init container as the above config. as you can see until the `DB is not started` init container keeps running and will not allow `application` container to start.

* Reference: [https://kubernetes.io/docs/concepts/workloads/pods/init-containers/](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)
    
* Reference: [https://github.com/m3pratik/31daysofEKS/](https://github.com/m3pratik/31daysofEKS/tree/main/day-13-kubenetes-secret)
    

Made with ❤️ by [**Pratikkumar Panchal**](https://www.linkedin.com/in/m3pratik/). [**https://github.com/m3pratik/31daysofEKS**](https://github.com/m3pratik/31daysofEKS)


&#xa0;

<a href="#top">Back to top</a>
