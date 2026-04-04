# Labels
---
## Add labels to pods/create a pod named app-pod with label env=dev
```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    env: dev
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```

## List pods using label selectors/List only the pods with label env=dev
```bash
sudo kubectl get pods -l <key>=<value>
sudo kubectl get pods -l env=dev
sudo kubectl get pods -l env=dev,app=web
```

## Add labels to an existing pod
```bash
sudo kubecl label pod <pod-name> <key>=<value>
sudo kubecl label pod <pod-name> <key1>=<value1> <key2>=<value2>
sudo kubectl label pod <pod-name> -n <ns-name> <key>=<value>
```

## Change/Update label to an existing pod
```bash
sudo kubectl label pod <pod-name> <key>=<newvalue> --overwrite
```
- If label is not available it appends and keeps other same labels same
- If label is already available it will just change the value of matching key and keeps other labels as it is.

## List labels of Pods
```bash
sudo kubectl get pods --show-labels
sudo kubectl get pods <pod-name> --show-labels
```
