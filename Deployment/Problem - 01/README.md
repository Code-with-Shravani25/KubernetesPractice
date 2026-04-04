# Deployment
---
## Create a deployment with 3 replicas
```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
## Apply
```bash
sudo kubectl apply -f deployment.yaml
```
## Verify
```bash
sudo kubectl get pods
sudo kubectl get deployments
```
## Scale the deployment to 5 pods/replicas
```bash
sudo kubectl scale deployment <deployment-name> --replicas=5
```
## Perform rolling update to nginx:latest/ new image bersion
```bash
sudo kubectl set image deployment/<deploymnet-name> nginx=nginx:latest
```
## Check rollout status
```bash
sudo kubectl rollout status deplloyment <deployment-name>
```
## Verify new image
```bash
sudo kubectl describe deployment <deployment-name>
```


## Rollback to previous version
```bash
sudo kubectl rollout undo deployment <deployment-name>
```
## Verify rollout
```bash
sudo kubectl describe deployment <deployment-name>
```
