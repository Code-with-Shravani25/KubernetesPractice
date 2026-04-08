# Kubernetes Rolling Update Stuck - Troubleshooting & Resolution

When a rolling update gets stuck in Kubernetes, it usually means new pods are not becoming Ready or old pods are not terminating.

---

## 1. Check Deployment Status

```bash
kubectl get deploy
kubectl describe deploy <deployment-name>
```

### Look for:
- Desired vs Available replicas
- Conditions (Progressing, Available)
- Events section

---

## 2. Check Pods Status

```bash
kubectl get pods -o wide
```

### Common Issues:
- Pods in Pending state
- Pods in CrashLoopBackOff
- Pods not Ready

---

## 3. Describe Problematic Pod

```bash
kubectl describe pod <pod-name>
```

### Look for:
- Image pull errors
- Resource issues
- Scheduling failures

---

## 4. Check Pod Logs

```bash
kubectl logs <pod-name>
```

### Possible Issues:
- Application crash
- Misconfiguration
- Missing environment variables

---

## 5. Check Readiness & Liveness Probes

If probes fail:
- Pod never becomes Ready
- Rolling update gets stuck

```yaml
readinessProbe:
  httpGet:
    path: /health
    port: 80
```

### Fix:
- Correct endpoint
- Increase initialDelaySeconds

---

## 6. Check Resource Constraints

```bash
kubectl describe node
```

### Issues:
- Insufficient CPU/Memory
- Pods stuck in Pending

---

## 7. Check Image Issues

- Wrong image name/tag
- Private registry auth failure

```bash
kubectl describe pod <pod-name> | grep -i image
```

---

## 8. Check MaxUnavailable & MaxSurge

```yaml
strategy:
  rollingUpdate:
    maxUnavailable: 1
    maxSurge: 1
```

### Problem:
- maxUnavailable = 0 can block updates if new pods fail

---

## 9. Check Pod Disruption Budget (PDB)

```bash
kubectl get pdb
```

### Issue:
- Too strict PDB blocks pod termination

---

## 10. Fix & Resume Deployment

### Option 1: Fix issue and wait
- Once pods become healthy, rollout continues

### Option 2: Restart rollout

```bash
kubectl rollout restart deployment <deployment-name>
```

### Option 3: Rollback

```bash
kubectl rollout undo deployment <deployment-name>
```

---

## 11. Force Delete Stuck Pods (Last Option)

```bash
kubectl delete pod <pod-name> --force --grace-period=0
```

---

## Summary

- Rolling update stuck = new pods not Ready OR old pods not terminating
- Common causes:
  - Probe failure
  - Resource shortage
  - Image issues
  - PDB restrictions

---

## Interview Tip

**Short Answer:**
> "Rolling update gets stuck when new pods fail readiness or old pods can't terminate. We debug using kubectl describe, logs, check probes, resources, and fix or rollback the deployment."

