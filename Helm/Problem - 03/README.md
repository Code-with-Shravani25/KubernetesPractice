# Customize values.yaml
---
- Customizing values.yaml is where Helm becomes really powerful—you control how the app is deployed without changing the chart itself.

## Step 1: Get the default values.yaml
```bash
helm show values bitnami/nginx > values.yaml
```
- This downloads the default configuration file you can edit.
## Step 2: Modify values.yaml
- Open values.yaml and change what you need.
- Change replica count, Change service type, Set custom port, Set resource limits

## Step 3: Install using custom values
```bash
helm install my-nginx bitnami/nginx -f values.yaml
```
- Helm will now use your configuration instead of defaults.
## Step 4: Update existing release
```bash
helm upgrade my-nginx bitnami/nginx -f values.yaml
```
## Step 5: Verify changes
```bash
kubectl get pods
kubectl get svc
```
