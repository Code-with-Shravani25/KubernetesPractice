# Multiple Containers
---
## Single Container Pod
```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```
## Multiple container inside a pod
```bash
apiVersion: v1
kind: Pod
metadata:
  name: multiple-container-pod
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
  - name: container2
    image: busybox
    command: ["sh","-c","while true;do echo Hello;sleep 5;done"]
```
```bash
sudo kubectl exec -it <pod-name> -- sh
```
- This connects to a first container by default if it has multiple containers inside a pod and if it has a single container then it connects to it.
- To connect to particular container, if a pod has multiple containers inside it then:
```bash
sudo kubectl exec -it <pod-name> -c <container-name> -- /bin/bash
```
