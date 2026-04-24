# PersistentVolume and PersistentVolumeClaim
---
## PersistentVolume
---
- Think of it as disk/storage(EBS.NFS,azuredisk)
- It is a piece of storage in the cluster that exists independent of pods.
- It lives outside the pod.
- Data persists even if pod is deleted.
- Can be reused by multiple pods.

## PersistentVolumeClaim
---
- Think of like a request form for storage.
- A PVC is a request for storage by a pod.
- Kubernetes automatically binds PVC->PV
- Requests:
- Storage size (eg: 1G)
- Access mode (ReadWriteOnce,etc)

- Pod-->PVC-->PV-->Actual storage
- Admin creates PV, user creates a PVC, kubernetes matches PVC with suitable PV and pod uses PVC.

 ## Access Modes
 ---
- ReadWriteOnce (RWO) → Read/write by one node only
- ReadOnlyMany (ROX) → Read-only by many nodes
- ReadWriteMany (RWX) → Read/write by many nodes

## Create PV
---
```bash
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
      path: /mnt/data
```

## Create PVC
---
```bash
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```
## Verify Binding
```bash
sudo kubectl get pv
sudo kubectl get pvc
```
- Output should show:
- STATUS: BOUND.
