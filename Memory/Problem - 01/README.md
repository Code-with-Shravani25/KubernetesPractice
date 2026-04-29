# Create a pod that exceeds memory limit and observe behaviour
---
```bash
apiVersion: v1
kind: Pod
metadata:
  name: memory-demo
spec:
  containers:
  - name: memory-demo-container
    image: polinux/stress
    resources:
      requests:
        memory: "50Mi"
      limits:
        memory: "100Mi"
    commands: ["stress"]
args: ["-vm","1","--vm-bytes","200M","--vm-hang,"1"]
```

- args: ["-vm","1","--vm-bytes","200M","--vm-hang,"1"] : run 1 worker process, allocate 200MB memory and hold the memory
- Set the limit: 100Mi
- Container tries to use: 200Mi
- This exceeds the limit intentionally.
- On kubectl describe pod <podname> you'll see state: OOMkilled (out of memory killed)
- Reason: Container exceeded memory limit.
- kubectl get pod <podname> // output: CrashLoopBackOff or Error

- OOM killed happens when a container exceeds its memory limit and its terminated by linux OOM killer.

- polinux/stress: It’s a lightweight container that includes the Linux stress tool.Used to generate CPU, memory, I/O load artificially
