# Allow traffic only from a specific pod.
---
## Kubernetes NetworkPolicy
---
- It is a resource used to control which Pods can communicate with each other and how (ingress/egress).
- Ingress (incoming traffic): Who can access a pod
- Egress (outgoing traffic): Where a pod can send traffic
---
## NetworkPolicy YAML
---
```bash
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-only-frontend
spec:
  podSelector:
    matchLabels:
      app: backend   # target pod
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: frontend   # only this pod allowed
```
- It applies to pod with label app:backend
- Allows only from app: frontend
- Everything else: ❌ blocked automatically

 ## Create backend pod
 ```bash
kubectl run backend --image=nginx --labels app=backend
```
## Create frontend pod
```bash
kubectl run frontend --image=busybox --labels app=frontend -- sleep 3600
```
## Create another pod that needs to be blocked
```bash
kubectl run test --image=busybox -- sleep 3600
```
## Apply Policy
```bash
kubectl apply -f policy.yaml
```
## Test
```bash
kubectl exec -it frontend -- wget -O- http://backend-ip # Allowed
kubectl exec -it test -- wget -O- http://backend-ip # Blocked
```
