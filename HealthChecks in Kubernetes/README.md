# Health Checks in Kuberenets
---
- Kubernetes uses probes(test/check) to check if your application is healthy.
- There are mainly two types:
1. Liveness Probe
2. Readiness Probe
---
## 1. Liveness Probe (Is app alive)
---
- Checks if the application is still running properly.
- Is my app dead or stuck
- If liveness probe fails --> Kubernetes restarts the container
- Detects failure --> restart container
- Example Scenario:
  - App goes into infinte loop
  - App is hung/frozen
  - Memory leak causes app to stop responding

## 2. Readiness Probe (Is app ready)
---
- Checks if application is ready to serve traffic
- Can my app handle requests right now?
- If readiness probe fails --> Pod is removed from service
- No traffic is sent to it.
- Readiness probe will mark pod not ready --> stop traffic
- Example Scenario:
  - App is still starting
  - App depends on DB connection
  - App is overloaded temporarily 

---
- Liveness probe checks container health and restarts it if needed, while readiness probe controls whether a pod receives traffic via a Service.
- Liveness probe: Focus on internal health of the container
- Readiness probe: Focus on traffic routing via Services
- We need to define liveness and readiness probes explicitly in your YAML if you want Kubernetes to perform these health checks. They are not enabled by default.
- They are defined inside container specifications
- spec → containers → livenessProbe / readinessProbe

 ## Example in Pod
 ```bash
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
  - name: app
    image: nginx

    livenessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 10 #Kubernetes waits 5 seconds after the container starts before running the probe for the first time
      periodSeconds: 5 #Kubernetes runs the probe every 3 seconds after the first check

    readinessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 3
```
## Example insode deployment
```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:   # 👈 Pod template
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: app
        image: nginx

        livenessProbe:
          httpGet:
            path: /
            port: 80

        readinessProbe:
          httpGet:
            path: /
            port: 80
```
