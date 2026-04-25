# Autoscaling in kubernetes
---
- Autoscaling in Kubernetes means automatically adjusting resources based on load—so your app gets more capacity when traffic increases and scales down when it’s idle.
- There are three main types:
1. Horizontal Pod Autoscaler (HPA)
2. Vertical Pod Autoscaler (VPA)
3. Cluster Autoscaler

 1. Horizontal Pod Autoscaler (HPA)
- Scales the number of Pods (replicas)
- Example
  - CPU increases → more Pods created
  - CPU decreases → Pods reduced
- How it works
  - Watches metrics (CPU, memory, custom)
  - Uses metrics from: Metrics Server
  - Metrics Server: It is a lightweight component that collects CPU and memory usage from Pods and Nodes in a Kubernetes cluster.
  - Metrics server is NOT always installed by default — sometimes it is, sometimes you must install it yourself.
  - It is already present in manages kubernetes like EKS, AKS (azure), GKE (Google)
  - In self maanged clusters you need to install
  ## Why metrics server is required
- Metrics Server is required because it collects CPU and memory usage from nodes and pods and exposes it to the Kubernetes API.
- The Horizontal Pod Autoscaler depends on this data to make scaling decisions. Without Metrics Server, HPA cannot function and kubectl top commands will not work.
 ---
- To check metrics server installed in clusters:
```bash
kubectl get pods -n kube-system
```
- Look for metrics-server if present no need to install it, if not we need to insatll it.
- To install metrics-server
```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

2. Vertical Pod Autoscaler (VPA)
---
- Adjusts CPU & Memory of a Pod
- Example
  - Pod needs more memory → increase limit
  - Too much allocated → reduce it
---
3. Cluster Autoscaler
---
- Scales nodes (VMs) in the cluster
- Example
  - Pods pending (no space) → adds nodes
  - Nodes idle → removes nodes
---

