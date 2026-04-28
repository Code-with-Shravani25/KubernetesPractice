# Expose a deployment using ClusterIP
---
## Create Deployment
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
## Create ClusterIP service
```bash
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```
## Apply Service
```bash
sudo kubectl apply -f clusterip.yaml
```
## Verify Service
```bash
sudo kubectl get svc
```
## Test
```bash
sudo kubectl run test-pod --rm -it --image=busybox -- sh
wget -qO- http://<svc-name>
```
