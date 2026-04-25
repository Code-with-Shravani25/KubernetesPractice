# Install nginx using helm
---
## Step 1: Install helm
---
- Download by following the steps from browser.
## Step 2: Add Helm repository
- Helm uses chart repositories. We’ll use Bitnami.
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```
- update repo
```bash
helm repo update
```
## Step 3: Search for Nginx chart
```bash
helm search repo nginx
```
- You'll see something like: bitnami/nginx
## Step 4: Install Nginx (create a release)
```bash
helm install my-nginx bitnami/nginx
```
- What this does:
  - Creates a release named my-nginx
  - Deploys Nginx on Kubernetes
  - Creates Pods, Service, etc.

## Step 5: Verify installation
- Check helm release
```bash
helm list
```
- Check pods and service
```bash
kubectl get pods
kubectl get svc
```
## Step 6: Access Nginx
```bash
minikube service my-nginx
```
