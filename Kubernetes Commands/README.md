# ☸️ Basic Kubernetes Commands

---

## 📌 Cluster Information

```bash
kubectl cluster-info
kubectl version
kubectl get nodes
```

---

## 📦 Pods

```bash
kubectl get pods
kubectl get pods -o wide #gives details like pod ips
kubectl describe pod <pod-name>
kubectl delete pod <pod-name>
```

---

## 📁 Namespaces

```bash
kubectl get namespaces
kubectl create namespace <namespace-name>
kubectl delete namespace <namespace-name>
```

Run command in a specific namespace:

```bash
kubectl get pods -n <namespace-name>
```

---

## 🚀 Deployments

```bash
kubectl get deployments
kubectl create deployment <name> --image=<image>
kubectl scale deployment <name> --replicas=3
kubectl delete deployment <name>
```

---

## 🔄 Rolling Updates

```bash
kubectl set image deployment/<name> <container>=<image>
kubectl rollout status deployment/<name>
kubectl rollout undo deployment/<name>
```

---

## 🌐 Services

```bash
kubectl get services
kubectl expose deployment <name> --type=NodePort --port=80
kubectl delete service <service-name>
```

---

## 📊 Logs & Debugging

```bash
kubectl logs <pod-name>
kubectl logs -f <pod-name>
kubectl exec -it <pod-name> -- /bin/bash
kubectl describe pod <pod-name>
```

---

## 📂 ConfigMaps & Secrets

### ConfigMap

```bash
kubectl create configmap <name> --from-literal=key=value
kubectl get configmaps
```

### Secret

```bash
kubectl create secret generic <name> --from-literal=username=admin --from-literal=password=1234
kubectl get secrets
```

---

## 📈 Resource Usage

```bash
kubectl top nodes
kubectl top pods
```

---

## 📄 Apply & Delete YAML

```bash
kubectl apply -f file.yaml
kubectl delete -f file.yaml
```

---

## 🔍 Get All Resources

```bash
kubectl get all
kubectl get all -A
```

---

## 🛠️ Useful Shortcuts

```bash
kubectl get po
kubectl get svc
kubectl get deploy
kubectl get ns
```

---

## 🎯 Tips

- Use `-o wide` for detailed output  
- Use `-n <namespace>` to target a namespace  
- Use `--watch` to monitor changes live  

---

## 📚 Conclusion

These commands are essential for:

- Daily operations  
- Troubleshooting  
- Kubernetes interviews  
