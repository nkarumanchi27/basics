# Kubernetes deployments basics
This file contains useful information on kubernetes deployments.

## Create a Kubernetes POD using YAML file:

```
apiVersion: v1
kind: Pod
metadata:
  name: rss-site
  labels:
    app: web
spec:
  containers:
    - name: front-end
      image: nginx
      ports:
        - containerPort: 80
    - name: rss-reader
      image: nickchase/rss-php-nginx:v1
      ports:
        - containerPort: 88
```

- Here, we started of with API version which is v1 for POSs but might be something else for other k8s resources.
- Kind represents k8s resources, which could be a POD, Deployment, Job, Service, etc.
- metadata which talks about the name of the POD and the lebel we will use to identify the POD to K8s
- finally , we will specify the actual objects that make up the POD. this includes,Containers, memory requirements, storage volumes,network or other details.

### Kubectl commands to create a POD from the above YAML and deal with it.
```
> kubetl create -f POD.yaml
> kubectl get pods
> kubectl describe pod rss-site
> kubectl delete pod rss-site
```

## Steps to create a K8S deployment from YAML
Some of the reasons why deployments are essential include, 
- high availability of K8S workloads, 
- scaling up/down of workloads, 
- managing state-deployments can be paused, edited , rolledback, 
- expositing k8s workloads to outside world , like creating a service and connecting to applicaitons.

```
---
apiVersion : apps/v1
kind: deployment
metadata:
  name: rss-site
  labels:
    app: web
spec:
  replicas: 2
  selector:
    matchLabels:
      app: web
    template:
      metadata:
        labels:
          app: web
      spec:
        containers:
          - name: front-end
            image: nginx
            ports:
              - containerPort: 80
           - name: rss-reader
             image: nickchase/rss-php-nginx:v1
             ports:
               - containerPort: 88
---
```
      
