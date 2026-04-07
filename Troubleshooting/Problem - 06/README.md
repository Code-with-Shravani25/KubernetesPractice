# 🚀 Config Change Applied but Pod Not Updated – Debug Guide

## 📌 Overview
In Kubernetes, updating a **ConfigMap or Secret does NOT automatically restart Pods**.  
This guide explains why Pods don’t reflect configuration changes and how to fix it.

---

## 🧠 Why Pods Are Not Updated

### 🔹 1. Pods Do Not Restart Automatically
Kubernetes does NOT restart Pods when:
- ConfigMap is updated
- Secret is updated

👉 Pods keep running with old configuration

---

### 🔹 2. Environment Variables Are Static
If ConfigMap/Secret is used as **env variables**, values are loaded only at Pod startup.

Example:
```yaml
env:
- name: APP_ENV
  valueFrom:
    configMapKeyRef:
      name: app-config
      key: APP_ENV
```

👉 Updating ConfigMap will NOT update running Pods

---

### 🔹 3. Volume Mount Behavior
If ConfigMap is mounted as a volume:

```yaml
volumeMounts:
- name: config
  mountPath: /etc/config
```

👉 Files are updated automatically BUT:
- App must reload config
- Otherwise changes won’t reflect

---

### 🔹 4. Deployment Not Triggered
Kubernetes Deployment only rolls Pods when:
- Pod template changes

👉 Updating ConfigMap alone does NOT trigger rollout

---

## 🔍 How to Fix

### ✅ 1. Restart Pods Manually
```bash
kubectl delete pod <pod-name>
```

---

### ✅ 2. Restart Deployment
```bash
kubectl rollout restart deployment <deployment-name>
```

---

### ✅ 3. Trigger Rollout with Annotation
```bash
kubectl patch deployment <deployment-name>   -p '{"spec":{"template":{"metadata":{"annotations":{"date":"'$(date +%s)'"}}}}}'
```

---

### ✅ 4. Use Volume + App Reload
- Mount ConfigMap as volume
- Enable app reload (e.g., SIGHUP, auto-reload)

---

### ✅ 5. Use Tools (Advanced)
- Reloader
- Helm hooks
- Operators

---

## ⚠️ Common Mistakes

- Expecting automatic restart after ConfigMap change
- Using env variables for dynamic config
- Not triggering rollout
- App not reloading config

---

## 🎯 Interview Answer

“Config changes do not update Pods automatically because Kubernetes does not restart Pods on ConfigMap or Secret updates. Environment variables are static, and Deployments only trigger rollouts when Pod template changes. To apply changes, we restart Pods or trigger a rollout.”

---

## 🏁 Conclusion

👉 Always remember:
- ConfigMap update ≠ Pod restart
- Restart or rollout is required

Start with:
```bash
kubectl rollout restart deployment <deployment-name>
```
