# Create Cluster Role and Cluster Role Binding as user
---
## Create Cluster Role
```bash
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: pod-reader-cluster
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
```
## Create Cluster Role Binding
```bash
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: pod-reader-binding
subjects:
- kind: User
  name: john              # username (from kubeconfig / cert)
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: pod-reader-cluster
  apiGroup: rbac.authorization.k8s.io
```

## Apply
```bash
kubectl apply -f clusterrole.yaml
kubectl apply -f clusterrolebinding.yaml
```
## Verify
```bash
kubectl auth can-i list pods --as=john
```
