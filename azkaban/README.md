# 1. To convert to Kubernetes deployment - Install kompose
More information: https://kubernetes.io/docs/tools/kompose/user-guide/

```
$ brew install kompose
```

# 2. Alternatives for deploying on Kubernetes with kompose

## 2.1 Deploy docker compose file with kompose to Kubernetes
```
$ kompose up

We are going to create Kubernetes Deployments, Services and PersistentVolumeClaims for your Dockerized application. 
If you need different kind of resources, use the 'kompose convert' and 'kubectl create -f' commands instead. 

INFO Successfully created Service: redis          
INFO Successfully created Service: web            
INFO Successfully created Deployment: redis       
INFO Successfully created Deployment: web         

Your application has been deployed to Kubernetes. You can run 'kubectl get deployment,svc,pods,pvc' for details.
```
## 2.2 Deploy docker compose file with kompose to Kubernetes

### 2.2.1 Convert Docker Compose file to Kubernetes deploy format
```
$ kompose convert                        
INFO Kubernetes file "azkexec-service.yaml" created 
INFO Kubernetes file "azkweb-service.yaml" created 
INFO Kubernetes file "mysql-service.yaml" created 
INFO Kubernetes file "azkexec-deployment.yaml" created 
INFO Kubernetes file "azkweb-deployment.yaml" created 
INFO Kubernetes file "mysql-deployment.yaml" created 
```

### 2.2.2 Start services on Kubernetes
```
$ kubectl create -f azkexec-deployment.yaml,azkweb-deployment.yaml,mysql-deployment.yaml
```
