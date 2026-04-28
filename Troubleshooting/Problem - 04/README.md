# 🚀 Kubernetes Service Not Reachable – Debugging Guide

---

## 🧠 Concept

In Kubernetes, traffic flows like this:

Client → Service → Endpoints → Pod → Container

If a Service is not reachable, the issue lies somewhere in this chain.

---

## 🔍 Step-by-Step Debugging

### 1️⃣ Check Pod Status
Ensure Pods are running and ready:

kubectl get pods -o wide

Expected:
STATUS: Running  
READY: 1/1

---

### 2️⃣ Verify Container Port
Ensure your application is listening on the correct port.

---

### 3️⃣ Check Service Configuration

kubectl get svc  
kubectl describe svc <service-name>

---

### 4️⃣ Check Endpoints (Most Important 🚨)

kubectl get endpoints <service-name>

- If `<none>` → Label mismatch  
- If IP present → Service is mapped correctly  

---

### 5️⃣ Test Connectivity Inside Cluster

kubectl exec -it <pod-name> -- curl <service-name>

---

### 6️⃣ Check Service Type

- ClusterIP → Internal only  
- NodePort → NodeIP:Port  
- LoadBalancer → External access  

---

### 7️⃣ Check Network Policies

kubectl get networkpolicy

---

### 8️⃣ Verify Cluster Networking

kubectl get pods -n kube-system

---

## ⚠️ Common Issues

- Label mismatch  
- Wrong targetPort  
- Incorrect service type  
- Network policies blocking traffic  
- Application not listening  

---

## 🎯 Interview Answer

“To debug a service not reachable, I check pod status, validate service configuration, verify endpoints for label matching, test connectivity inside the cluster, and finally review service type and network policies.”

---

## 🏁 Conclusion

Start debugging with:

kubectl describe svc <service-name>  
kubectl get endpoints <service-name>
