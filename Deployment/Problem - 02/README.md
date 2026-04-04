# Generate a deployment YAML for httpd without creating it. (Means create YAML file but dont apply)
```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: httpd
  template:
    metadata:
      labels:
        app: httpd
    spec:
      containers:
      - name: httpd
        image: httpd:latest
        ports:
        - containerPort: 80
```
## Apply
```bash
sudo kubectl apply -f deployment.yaml
```

## Verify
```bash
sudo kubectl exec -it <pod-name> -- /bin/bash
apt update
apt install curl -y
curl http://localhost #To check apache web page
```
