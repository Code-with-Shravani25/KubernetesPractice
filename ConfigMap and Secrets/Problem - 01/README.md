# ConfigMap
---
- A ConfigMap in Kubernetes is a way to store configuration data (like key-value pairs) separately from your application code.
- Instead of hardcoding configs inside your container, you keep them in a ConfigMap and inject them into your pods when needed.

---
## Create configmap with key APP_ENV=production
```bash
apiVersion: v1
kind: ConfigMap
metadata:
  name: game-demo
data:
  APP_ENV: production
```

---
## Apply
```bash
sudo kubectl apply -f configmap.yaml
```

## Verify
```bash
sudo kubectl get configmap <configname>
sudo describe configmap <configname>
```
