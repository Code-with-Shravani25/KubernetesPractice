# Deploy an nginx pod in the particular namespace
---
## Using command
```bash
sudo kubectl run <podname> --image=nginx:latest -n <ns-name>
```
## Verify
```bash
sudo kubectl get pods -n <ns-name>
```

## Using YAML
```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: app-ns
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
```
## Apply
```bash
sudo kubectl apply -f pod.yaml
```
