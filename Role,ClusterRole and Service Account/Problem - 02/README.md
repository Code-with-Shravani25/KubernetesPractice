# Create Role and Role Binding as service account
---
## Service Account
---
```bash
kubectl create serviceaccount dev-sa
```
or 
```bash
apiVersion: v1
kind: ServiceAccount
metadata:
  name: demo-sa
  namespace: default
```
## Role
```bash
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: default
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
```
## RoleBinding
```bash
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: pod-reader-binding
  namespace: default
subjects:
- kind: ServiceAccount
  name: demo-sa
  namespace: default
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```
## Apply
```bash
kubectl apply -f role.yaml
kubectl apply -f rolebinding.yaml
```

## Verify
```bash
kubectl auth can-i list pods --as=system:serviceaccount:default:demo-sa
```
