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
      
- here *API version*: specifies that we want a deployment
- as part of the pod spec *replicas*, we are saying what ever the pods we deploy we want two replicas.
- *selector* specifies the pods effected by this deploument, we are selecting pods by their label.
- *templates* parameter specifies the 2 replicas of what , 
### k8s commands to create a deployment from above deployment.yaml file.
```
> kubectl create -f deployment.yaml
> kubectl get deployments
> kubectl describe deployment rss-site
a simple way to updating the properties of a deployment involves editing the yaml file used for the deployment. to do this, we always want to use *apply* command instead of *create*.
> kubectl apply -f deployment.yaml
some of the other options are
> kubectl edit deployment.v1.apps/rss-site
> kubectl scale deployment.vs.apps/rss-site --replicas=5
> kubectl autoscale deployment.v1.apps/rss-site --min=3 --max=20 --cpu-percent=60
