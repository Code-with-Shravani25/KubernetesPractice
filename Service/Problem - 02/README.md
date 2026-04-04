# Expose a deployment using NodePort
---
## Create deployment and apply
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
## Create a NodePort Service
```bash
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```
## Apply Service
```bash
sudo kubectl apply -f service.yaml
```
## Verify
```bash
sudo kubectl get nodes -o wide #here in external will get ip but if using minikube it will be none
```
- Minikube runs inside a private network of EC2, so nodeport ip is not directly accessible from outside.
- As minikube is designed for local development, not for public exposure.
```bash
sudo minikube service <service-name>
curl <url>
```
