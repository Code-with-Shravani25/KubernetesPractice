# Use port forward to access the app
---
- Port forwarding in Kubernetes allows you to access a pod or service locally (from your machine) without exposing it externally.

- 👉 It creates a temporary tunnel between:
- your local machine port
- and a port inside the pod/service

- 🧠 Simple Understanding
- Instead of exposing your app using NodePort / LoadBalancer, you can do:
- 👉 “Take my localhost port and connect it directly to a pod”

## Port forward to Pod
```bash
kubectl port-forward pod/<pod-name> 8080:80
```

## Port forward to Service
```bash
kubectl port-forward svc/<service-name> 8080:80
```

## To verify: open another terminal and check
```bash
http://localhost:8080
```
