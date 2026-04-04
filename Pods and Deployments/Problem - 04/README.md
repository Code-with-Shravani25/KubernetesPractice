# Some Commands
---
## Get detailed description of pod for particular namespace
```bash
sudo kubectl describe <pod-name> -n <ns-name>
```
## Get detailed description of pod for default namespace
```bash
sudo kubectl describe <pod-name>
```
- In container section you will get containers,image,port,state
- In events section you will get lifecycle of pod, errors and scheduling details

## Delete the pod using a single command for default namespace
```bash
sudo kubectl delete pod <pod-name>
```
## Delete the pod using a single command for particular namespace
```bash
sudo kubectl delete pod <pod-name> -n <ns-name>
```

## Exec into a running pod and check nginx config for default namespace
```bash
sudo kubectl exec -it <pod-name> -- /bin/bash
cat /etc/nginx/nginx.conf
```
## Exec into a running pod and check nginx config for particular namespace
```bash
sudo kubectl exec -it <pod-name> -n <ns-name> -- /bin/bash
cat /etc/nginx/nginx.conf
```

## Get pods from all namespaces
```bash
sudo kubectl get pods -A
```

## Show only pod names in output
```bash
sudo kubectl get pods -o jsonpath="{.items[*].metadata.names}
```
