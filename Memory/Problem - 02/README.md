# Set CPU and Memory requests and limits
---
```bash
apiVersion: v1
kind: Pod
metadata:
  name: resource-demo
spec:
  containers:
  - name: mycontainer
    image: nginx
    resources:
      requests:
        cpu: "250m"      # 0.25 CPU
        memory: "128Mi"
      limits:
        cpu: "500m"      # 0.5 CPU
        memory: "256Mi"
```
- requests tells minimum guarantee, k8s guarantee this much resource and scjeduler uses this to decide which node to place the pod on.
- limits tells maximum allowed, container cannot exceed this and if exceeded memory then OOMkilled
- CPU--> throttled(slowed down)
