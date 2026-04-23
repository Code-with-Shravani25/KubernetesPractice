# Create a secret and mount a volume to pod
---

## Step 1: Create a Secret YAML

Create a file named secret.yaml
```bash
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: ZGV2b3Bz
  password: ZGV2b3BzMTIz
```
## Step 2: Apply the Secret
```bash
kubectl apply -f secret.yaml
```
## Step 3: Verify Secret Creation
```bash
kubectl get secrets
kubectl describe secret my-secret
```
## Step 4: Create Pod YAML with Secret Volume

Create a file named pod.yaml
```bash
apiVersion: v1
kind: Pod
metadata:
  name: secret-volume-pod
spec:
  containers:
  - name: mycontainer
    image: nginx
    volumeMounts:
    - name: secret-volume
      mountPath: /etc/secret
      readOnly: true
  volumes:
  - name: secret-volume
    secret:
      secretName: my-secret
```
## Step 5: Apply the Pod
```bash
kubectl apply -f pod.yaml
```
## Step 6: Verify Pod is Running
```bash
kubectl get pods
```
## Step 7: Access the Pod
```bash
kubectl exec -it secret-volume-pod -- /bin/sh
```
## Step 8: Verify Secret Inside Container
```bash
cd /etc/secret
ls

cat username
cat password

Expected Output:
devops
devops123
```
