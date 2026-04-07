# Kubernetes Deployment Failing - Root Cause & Fix Guide

When a Deployment is failing in Kubernetes, follow this structured approach to identify the root cause and fix it.

---

## 1. Check Deployment Status
```bash
kubectl get deployments
kubectl describe deployment <deployment-name>
```

Look for:
- Available replicas vs desired replicas
- Events section (very important)

---

## 2. Check ReplicaSet
```bash
kubectl get rs
kubectl describe rs <replicaset-name>
```

Issues:
- ReplicaSet not creating pods
- Errors in events

---

## 3. Check Pods
```bash
kubectl get pods
kubectl describe pod <pod-name>
```

Look for:
- Pod status (CrashLoopBackOff, Pending, Error)
- Events at the bottom

---

## 4. Check Pod Logs
```bash
kubectl logs <pod-name>
```

If multiple containers:
```bash
kubectl logs <pod-name> -c <container-name>
```

Common issues:
- Application crash
- Missing environment variables
- Port binding issues

---

## 5. Common Failure Scenarios & Fixes

### 5.1 Image Pull Error
**Error:** ImagePullBackOff / ErrImagePull

**Cause:**
- Wrong image name
- Private registry authentication issue

**Fix:**
```bash
kubectl describe pod <pod-name>
```
- Verify image name
- Add imagePullSecrets if needed

---

### 5.2 CrashLoopBackOff
**Cause:**
- Application crashing repeatedly

**Fix:**
- Check logs
- Fix application issue
- Verify configs, env variables

---

### 5.3 Pod Pending
**Cause:**
- Insufficient resources
- Node selector/taints issues

**Fix:**
```bash
kubectl describe pod <pod-name>
```
- Check scheduling errors
- Add resources or fix node constraints

---

### 5.4 Liveness/Readiness Probe Failure
**Cause:**
- Health checks failing

**Fix:**
- Correct probe path/port
- Increase timeout/delay

---

### 5.5 ConfigMap / Secret Issue
**Cause:**
- Missing or incorrect configuration

**Fix:**
```bash
kubectl get configmap
kubectl get secrets
```
- Validate keys and values

---

### 5.6 Volume Mount Failure
**Cause:**
- PVC not bound or storage issue

**Fix:**
```bash
kubectl get pvc
kubectl describe pvc
```

---

### 5.7 Port Conflict
**Cause:**
- Application trying to use a busy port

**Fix:**
- Change container port
- Update service configuration

---

## 6. Check Events (Most Important)
```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

---

## 7. Rollback Deployment
If issue after new release:

```bash
kubectl rollout undo deployment <deployment-name>
```

---

## 8. Restart Deployment
```bash
kubectl rollout restart deployment <deployment-name>
```

---

## 9. Verify Fix
```bash
kubectl get pods
kubectl get deployments
```

Ensure:
- Pods are Running
- READY = desired count

---

## Quick Troubleshooting Flow

1. Deployment → `describe`
2. ReplicaSet → check
3. Pods → status + describe
4. Logs → identify crash
5. Events → root cause
6. Fix → config/image/resources
7. Rollback if needed

---

## Interview Tip

**One-line answer:**
> "To debug a failing deployment, I check deployment, ReplicaSet, pods, logs, and events to find the root cause, then fix configuration, image, or resource issues and verify rollout."

