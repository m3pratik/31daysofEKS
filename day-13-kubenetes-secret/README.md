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

A Secret is an object that contains a small amount of sensitive data such as a `password`, a `token`, or a `key`.

In our previous blog, we create a deployment of the `PostgreSQL` database.

Remember, on that blog we use env in the below format:

```yaml
          env:
            - name: POSTGRES_USER
              value: postgres
            - name: POSTGRES_PASSWORD
              value: postgres123
```

**This is not a recommended way to manage the** `secrets` **, it can be easily read by anyone.**

So there is a solution provided by Kubernetes to manage the `secrets` like above.

* Reference: [https://kubernetes.io/docs/concepts/configuration/secret/](https://kubernetes.io/docs/concepts/configuration/secret/)
    

### (1) Create a Secret.

The values for all keys in the `data` the field has to be base64-encoded strings.

to create your secret data into base64 , there are two ways.

1. On Linux/Mac `echo -n 'dbpassword11' | base64`
    
2. Online tool: [https://codebeautify.org/base64-encode](https://codebeautify.org/base64-encode)
    

For example in below example we converted secret text `postgres123` to `base64` text.  
`echo -n 'postgres123' | base64`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1674127096164/f5e6d4e2-8b94-41f1-8a64-85b94444de59.png align="center")

### (2) Create Secrets manifest.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: postgres-db-envs
type: Opaque
data:
  POSTGRES_USER: cG9zdGdyZXM=
  POSTGRES_PASSWORD: cG9zdGdyZXMxMjM=
```

### (3) Update Deployment Env configs.

```yaml
          env:
            - name: POSTGRES_USER
              valueFrom:
                secretKeyRef:
                  name: postgres-db-envs
                  key: POSTGRES_USER
            - name: POSTGRES_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: postgres-db-envs
                  key: POSTGRES_PASSWORD
```

As you can see in the above file, Because Secrets can be created independently of the Pods that use them, there is less risk of the Secret (and its data) being exposed during the workflow of creating, viewing, and editing Pods. Kubernetes, and applications that run in your cluster, can also take additional precautions with Secrets, such as avoiding writing secret data to nonvolatile storage.

\*Reference: [https://kubernetes.io/docs/concepts/configuration/secret/](https://kubernetes.io/docs/concepts/configuration/secret/)

Made with ❤️ by [**Pratikkumar Panchal**](https://www.linkedin.com/in/m3pratik/). [**https://github.com/m3pratik/31daysofEKS**](https://github.com/m3pratik/31daysofEKS)


&#xa0;

<a href="#top">Back to top</a>
