# Namespace

---
## Create a namespace
```bash
sudo kubectl create namespace <namespace-name>
```

## Verify
```bash
sudo kubectl get namespaces
```
## Create namespace using yaml
```bash
apiVersion: v1
Kind: Namespace
metadata:
  name: aap-ns
```

## Apply
```bash
sudo kubectl apply -f namespace.yaml
```
