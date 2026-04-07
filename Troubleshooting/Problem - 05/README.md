# 🚀 App is Running but Traffic Not Reaching It – Debug Guide

## 📌 Overview
This guide helps troubleshoot situations where a Kubernetes **application is running but not receiving traffic**.

---

## 🧠 Concept

Traffic flow in Kubernetes:

Client → Service → Endpoints → Pod → Container

---

## 🔍 Step-by-Step Debugging

### 1️⃣ Check Pod Status
```bash
kubectl get pods -o wide
```

Ensure:
- STATUS: Running
- READY: 1/1

---

### 2️⃣ Check Application Inside Pod
```bash
kubectl exec -it <pod-name> -- sh
curl localhost:<port>
```

If it fails → App not listening or wrong port

---

### 3️⃣ Verify Container Port
```yaml
ports:
- containerPort: 80
```

Must match application port

---

### 4️⃣ Check Service Configuration
```bash
kubectl get svc
kubectl describe svc <service-name>
```

Verify:
- port
- targetPort

---

### 5️⃣ 🚨 Check Endpoints (Most Important)
```bash
kubectl get endpoints <service-name>
```

#### ❌ No Endpoints
```
<none>
```
Cause: Label mismatch

Fix:
```yaml
# Pod
labels:
  app: myapp

# Service
selector:
  app: myapp
```

---

#### ✅ Endpoints Present
```
10.244.0.5:80
```

---

### 6️⃣ Test Inside Cluster
```bash
kubectl run test --rm -it --image=busybox -- sh
wget -qO- http://<service-name>
```

---

### 7️⃣ Check Service Type

| Type | Access |
|------|--------|
| ClusterIP | Internal only |
| NodePort | NodeIP:Port |
| LoadBalancer | External |

---

### 8️⃣ Check Ingress
```bash
kubectl get ingress
```

Verify host and backend service

---

### 9️⃣ Check Network Policies
```bash
kubectl get networkpolicy
```

---

### 🔟 Check Firewall / Security Groups
Ensure ports are open (NodePort / LoadBalancer)

---

## ⚠️ Common Issues

- Label mismatch
- Wrong port mapping
- ClusterIP used for external access
- Network policies blocking traffic
- App not listening

---

## 🎯 Interview Answer

“To debug this issue, I check pod health, verify application port, validate service configuration, ensure endpoints are correct, test inside cluster, and then check service type, ingress, and network policies.”

---

## 🏁 Conclusion

Start with:
```bash
kubectl describe svc <service-name>
kubectl get endpoints <service-name>
```
