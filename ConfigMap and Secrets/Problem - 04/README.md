# Use configmap as mounted volume
---
## Create configmap
```bash
apiVersion: v1
kind: ConfigMap
metadata:
  name: myconfigmap
data:
  APP_ENV: production
  APP_DEBUG: "false"
```
## Apply
```bash
kubectl apply -f configmap.yaml
```
## Mountedvolume
```bash
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mypod
    image: redis
    volumeMounts:
    - name: configvolume  # same name as below
      mountPath: "/etc/config"
  volumes:
  - name: configvolume
    configMap:
      name: myconfigmap
```
## Apply
```bash
sudo kubectl apply -f mountedvolume.yaml
```
---
## What happens here
- Configmap app-config  converted into files mounted at /etc/config

 ## Verify
 ```bash
sudo kubectl exec -it <podname> -- /bin/bash
/etc/config/APP_ENV # inside container
```
