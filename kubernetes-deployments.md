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

_Here, we started of with API version which is v1 for POSs but might be something else for other k8s resources._
_ Kind represents k8s resources, which could be a POD, Deployment, Job, Service, etc._



