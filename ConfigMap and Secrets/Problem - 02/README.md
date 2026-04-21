# Create ConfigMap from literals and file
---
## Create Configmap from Literals
```bash
kubectl create configmap <name> --from-literal=APP_ENV=production --from-literal=APP_DEBUG=false
```
---
## Create Config map from file
- To create configmap from a file we can use: config.txt, env,settings.conf,myfile,app.properties
- Any extension and any name works.

## app.txt
```bash
APP_ENV=production
APP_DEBUG=false
```

## Create configmap from file
```bash
sudo kubectl create configmap app-config-file --from-file=app.txt
```

## Verify
```bash
kubectl get configmap
kubectl describe configmap <configmap-name> -file
```

- --from-literal : Direct key value pairs
- --from-literal : Stores file content as value
