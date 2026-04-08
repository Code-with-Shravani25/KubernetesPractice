# Kubernetes Volumes - Complete Guide

## 📌 Introduction

Containers in Kubernetes are **ephemeral**, meaning data is lost when a Pod restarts or is deleted.

👉 **Volumes** solve this problem by providing **persistent and shared storage**.

---

## 🔹 What is a Volume?

A **Volume** is a directory that:
- Is accessible to containers in a Pod
- Persists beyond container lifecycle
- Can be shared between containers in the same Pod

---

## 🔹 Basic Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-demo
spec:
  containers:
  - name: app
    image: nginx
    volumeMounts:
    - name: my-volume
      mountPath: /usr/share/nginx/html
  volumes:
  - name: my-volume
    emptyDir: {}
```

---

## 🔹 Types of Volumes

### 1. emptyDir
- Temporary storage
- Deleted when Pod is removed
- Used for cache, temp data

```yaml
volumes:
- name: temp-storage
  emptyDir: {}
```

---

### 2. hostPath
- Uses node filesystem
- Not portable

```yaml
volumes:
- name: host-volume
  hostPath:
    path: /data
```

⚠️ Avoid in production

---

### 3. ConfigMap Volume
- Inject configuration as files

```yaml
volumes:
- name: config-vol
  configMap:
    name: app-config
```

---

### 4. Secret Volume
- Store sensitive data

```yaml
volumes:
- name: secret-vol
  secret:
    secretName: my-secret
```

---

### 5. PersistentVolume (PV)
- Real storage (disk, cloud, etc.)
- Independent of Pod lifecycle

---

### 6. PersistentVolumeClaim (PVC)
- Request for storage
- Used by Pods

---

## 🔁 PV + PVC Flow

```
Pod → PVC → PV → Storage
```

---

## 🔹 PVC Example

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

## 🔹 Pod Using PVC

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pvc-pod
spec:
  containers:
  - name: app
    image: nginx
    volumeMounts:
    - mountPath: /data
      name: storage
  volumes:
  - name: storage
    persistentVolumeClaim:
      claimName: my-pvc
```

---

## 🔹 Access Modes

- ReadWriteOnce (RWO)
- ReadOnlyMany (ROX)
- ReadWriteMany (RWX)

---

## 🔹 Key Differences

| Feature | emptyDir | PVC |
|--------|---------|-----|
| Persistence | No | Yes |
| Lifecycle | Pod | Independent |
| Use Case | Temp data | Databases |

---

## 🔹 Real Use Cases

- Databases → PVC
- Logs sharing → emptyDir
- Config → ConfigMap
- Secrets → Secret

---

## 🔹 Common Mistakes

- Using emptyDir for databases ❌
- Using hostPath in production ❌
- Forgetting volumeMounts ❌

---

## 🔹 Debugging Commands

```bash
kubectl describe pod <pod-name>
kubectl exec -it <pod> -- ls /mount/path
kubectl get pvc
kubectl get pv
```

---

## 🔹 Summary

> Volumes in Kubernetes allow data persistence and sharing across containers, overcoming the ephemeral nature of containers.

