# Create Cluster Role and Cluster Role Binding as user
---
## Create ServiceAccount
```bash
apiVersion: v1
kind: ServiceAccount
metadata:
  name: demo-sa
  namespace: default
```
## ClusterRole
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
## ClusterRole Binding
```bash
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: pod-reader-binding-cluster
subjects:
- kind: ServiceAccount
  name: demo-sa
  namespace: default
roleRef:
  kind: ClusterRole
  name: pod-reader-cluster
  apiGroup: rbac.authorization.k8s.io
```
---
## Apply
```bash
kubectl apply -f sa.yaml
kubectl apply -f clusterrole.yaml
kubectl apply -f clusterrolebinding.yaml
```
## Verify
```bash
kubectl auth can-i list pods --as=system:serviceaccount:default:demo-sa
```
