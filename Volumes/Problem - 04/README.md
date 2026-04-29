# HostPath Volume
---
- A hostPath volume is a type of volume that mounts a file or directory from the node (host machine) into a Pod.
## Create a pod with hostpath volume
---
```bash
apiVersion: v1
kind: Pod
metadata:
  name: hostpath-pod
spec:
  containers:
  - name: mycontainer
    image: nginx
    volumeMounts:
    - name: host-volume
      mountPath: /usr/share/nginx/html
  volumes:
  - name: host-volume
    hostPath:
      path: /data   # path on the node
      type: DirectoryOrCreate # creates automatically if missing or else uses the existing
```
## Apply
```bash
sudo kubectl apply -f hostpath.yaml
```
## Verify
```bash
sudo kubectl exec -it hostpath-pod -- sh
ls /data
cat /data/file.txt
```
- Delete pod, reapply and check again
```
