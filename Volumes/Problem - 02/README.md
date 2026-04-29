# EmptyDir Volume
---
- When pod is deleted data is also lost if using conntainers file system (default), emptyDir Volume.
- Data is not lost if using PV,PVC,hostpath.
- emptyDir is a temporary volume that is created when a pod starts and deleted when pod is removed.
- It shares between all containers in the same pod.
---

## Create a pod with emptyDir volume
```bash
apiVersion: v1
kind: Pod
metadata:
  name: emptydir-pod
spec:
  containers:
    - name: container1
      image: nginx
      volumeMounts:
        - name: shared-data
          mountPath: /usr/share/nginx/html
    - name: container2
      image: busybox
      command: ["sleep","3600"]
      volumeMounts:
        - name: shared-data
          mountPath: /data
  volumes:
    - name: shared-data
      emptyDir: {}
```
## Verify
```bash
sudo kubectl exec -it <podname> -c container1 -- /bin/bash
```
- Create a file under /usr/share/nginx/html
- Verify it in container at /data location
- Delete a pod and reapply the yaml
- exec into any container and check the data
- Data exists if pod was running and data lost after pod deletion.
