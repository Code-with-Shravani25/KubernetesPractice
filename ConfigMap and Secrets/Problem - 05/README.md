# Create a Secret and inject it in pod
---
## Secrets.yaml
```bash
apiVersion: v1
kind: Secret
metadata:
  name: secret-sa-sample
type: Opaque
data:
  username: ZGV2b3Bz #Encoded in base64, to encode echo -n "devops" | base64
  password: ZGV2b3BzMTIz #echo -n "devops123" | base64
```

## Apply
```bash
sudo kubectl apply -f secrets.yaml
```
## Inject secret inside a pod
```bash
apiVersion: v1
kind: Pod
metadata:
  name: env-single-secret
spec:
  containers:
  - name: envars-test-container
    image: nginx
    env:
    - name: SECRET_USERNAME
      valueFrom:
        secretKeyRef:
          name: secret-sa-sampl #secret name
          key: backend-username
    - name: SECRET_PASSWORD
      valueFrom:
        secretKeyRef:
          name: secret-sa-sampl #secret name
          key: backend-username
```

## Verify
```bash
sudo kubectl get secrets
kubectl exec -it env-single-secret -- /bin/sh #inside container
printenv | grep SECRET
```

## To Decode
```bash
echo ZGV2b3Bz | base64 --decode
echo ZGV2b3BzMTIz | base64 --decode
```
