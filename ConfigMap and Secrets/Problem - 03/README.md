# Mount the configmap inside a pod as an env variable
---
## Create configmap
```bash
apiVersion: v1
kind: ConfigMap
metadata:
  name: game-demo
data:
  APP_ENV: production
```
---
## Apply
```bash
sudo kubectl apply -f configmap.yaml
```
---
## Create a pod that mounts the specific key of configmap
```bash
apiVersion: v1
kind: Pod
metadata:
  name: configmap-demo-pod
spec:
  containers:
    - name: demo
      image: alpine
      command: ["sleep", "3600"]
      env:
        - name: PLAYER_INITIAL_LIVES # Use this name to verify
          valueFrom:
            configMapKeyRef:
              name: game-demo           # The name of configmap
              key: player_initial_lives
```
## Create a pod that imports all keys
```bash
apiVersion: v1
kind: Pod
metadata:
  name: env-configmap
spec:
  containers:
    - name: app
      command: ["/bin/sh", "-c", "printenv"]
      image: busybox:latest
      envFrom:
        - configMapRef:
            name: game-demo 
```
---
## Verify
```bash
sudo kubectl exec -it <pod-name> -- env | grep APP_ENV
```
or
```bash
sudo kubectl exec -it <pod name> -- /bin/bash
echo $<env-name> #echo $PLAYER_INITIAL_LIVES
```
