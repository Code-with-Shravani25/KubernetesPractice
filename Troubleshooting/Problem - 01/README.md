# CrashLoopBackOff

- CrashLoopBackOff means kubernetes tries to restart a container multiple times, but it keeps crashing.
- Container inside pod keeps crashing repeatedly in loop.
 
---
## Create a pod that crashes intentionally and check.

```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    command: ["sh","-c","echo Crash Test && exit 1"]
```

## Apply
```bash
sudo kubectl apply -f crash-pod.yaml
```

## Verify
```bash
sudo kubectl get pods #Status: Error
sudo kubectl describe pod crash-pod #Event section
```
