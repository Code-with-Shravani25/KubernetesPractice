# Deny traffic using network policy
---
## Deny all traffic (Both Ingress and Egress)
---
```bash
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all
spec:
  podSelector: {}   # applies to ALL pods in namespace
  policyTypes:
  - Ingress
  - Egress
```
## Apply
```bash
kubectl apply -f deny-all.yaml
```
- What happens now?
- ❌ No pod can receive traffic
- ❌ No pod can send traffic
- ❌ Even DNS may fail
---
## Deny ONLY incoming traffic (Ingress)
```bash
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-ingress
spec:
  podSelector: {}
  policyTypes:
  - Ingress
```
## Apply
```bash
kubectl apply -f deny-ingress.yaml
```
- What happens
- ❌ No pod can be accessed
- ✔ Pods can still send requests out

 ## Deny ONLY outgoing traffic (Egress)
 ```bash
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-egress
spec:
  podSelector: {}
  policyTypes:
  - Egress
```
## Apply
```bash
kubectl apply -f deny-egress.yaml
```
- What happens
- ✔ Pods can receive traffic
- ❌ Cannot call other pods / internet

## Test
- Create two pods
```bash
kubectl run pod-a --image=nginx
kubectl run pod-b --image=busybox -- sleep 3600
```
- Test before policy
```bash
kubectl exec -it pod-b -- wget -O- http://pod-a-ip #works
```
- Apply policy
- Test again
```bash
kubectl exec -it pod-b -- wget -O- http://pod-a-ip #fails
```
