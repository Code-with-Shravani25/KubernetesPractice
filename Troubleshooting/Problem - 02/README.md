# Pod Stuck in Pending State
- A Pod stuck in Pending means Kubernetes has accepted the Pod but has not been able to schedule or start it on a node yet.
- Think of it like: “Pod created, but Kubernetes can’t find a suitable place or resources to run it.”
- Pending = Scheduling Problem (Not an container issue)

## Achieve a Pod stuck in pending state, by either requesting more resources than available, or using wrong node selector.
```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    resources:
      requests:
         memory: "100Gi"
         cpu: "10"
```

## Apply:
```bash
sudo kubectl apply -f pending-pod.yaml
```

## Verify:
```bash
sudo kubectl get pods
sudo kubectl describe pod pending-pod.yaml #Event Section
```
