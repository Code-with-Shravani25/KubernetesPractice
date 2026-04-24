# Create Role and Role Binding using user
---

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
  name: read-pods-binding
  namespace: default
subjects:
- kind: User
  name: dev-user        # user name
  apiGroup: rbac.authorization.k8s.io
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
kubectl get roles
kubectl get rolebindings
```

## Test
```bash
kubectl auth can-i list pods --as=dev-user
```

