# Enable HPA for a deployment
---
## Create deployment that has CPU requests defined
---
```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: nginx
        image: nginx
        resources:
          requests:
            cpu: "100m"
          limits:
            cpu: "200m"
```
## Apply
---
```bash
kubectl apply -f deployment.yaml
```
## Enable HPA
---
```bash
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: my-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  minReplicas: 1
  maxReplicas: 5
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
```
## Apply
```bash
kubectl apply -f hpa.yaml
```
## Verify HPA
```bash
kubectl get hpa
```
## Test Autoscaling
- Generate load
```bash
kubectl run -i --tty load-generator --image=busybox -- /bin/sh
```
Inside
```bash
while true; do wget -q -O- http://my-app; done
```
Watch Scaling
```bash
kubectl get hpa -w
```
