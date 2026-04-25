# Create Service Account and attach it to Pod.
---
## Create Service Account
```bash
apiVersion: v1
kind: ServiceAccount
metadata:
  name: demo-sa
  namespace: default
```
## Create a Pod
```bash
apiVersion: v1
kind: Pod
metadata:
  name: sa-pod
spec:
  serviceAccountName: demo-sa   # attach SA here
  containers:
  - name: mycontainer
    image: nginx
```
## Apply
```bash
kubectl apply -f sa.yaml
kubectl apply -f pod.yaml
```
## Verify
```bash
kubectl describe pod sa-pod # look for Service Account:  demo-sa
```
