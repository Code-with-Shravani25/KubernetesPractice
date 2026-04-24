# Create a pod with CPU limit 500m and memory limit 256Mi
---
```bash
apiVersion: v1
kind: Pod
metadata:
  name: limit-demo
spec:
  containers:
  - name: nginx-container
    image: nginx
    resources:
      limits:
        cpu: "500m"
        memory: "256Mi"
```
## Verify by generating CPU load inside container
```bash
kubectl exec -it cpu-test -- /bin/bash
yes > /dev/null
```
