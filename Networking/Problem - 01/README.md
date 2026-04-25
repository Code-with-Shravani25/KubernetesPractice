# Networking in Kubernetes
---
- Kubernetes networkung follows one simple rule that is evry pod can talk yo every other pod directly using ip (by default) if they are in same cluster.
- Pods in same cluster can communicate with each other, even if they are on different nodes, but needs to be in same cluster.
- Pods in same kubernetes cluster can communicate with each other across nodes using their IPz, as long as there is no NetworkPolicies or network restrictions are applied.
- Pods can communicate freely within same kubernetes cluster, even across nodes but cannot communicate across different clusters unless additional networking or exosure is configured.
---
## Create two pods and test connectivity between them.
---
## Step 1: Create Pod1
```bash
apiVersion: v1
kind: Pod
metadata:
  name: pod-1
  labels:
    app: test
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```

## Step 2: Create Pod2
---
```bash
apiVersion: v1
kind: Pod
metadata:
  name: pod-2
spec:
  containers:
  - name: busybox
    image: busybox
    command: ["sleep", "3600"]
```

## Step 3: Apply
```bash
kubectl apply -f pod1.yaml
kubectl apply -f pod2.yaml
```

## Get IP
```bash
kubectl get pods -o wide
```

## Exec into pod 2
```bash
kubectl exec -it pod-2 -- sh
```

## Test inside pod2
```bash
wget -O- http://<POD-1-IP>
```
or
```bash
ping <POD-1-IP>
```

