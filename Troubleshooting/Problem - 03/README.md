# ImagePullBackOff

- ImagePullBackOff: A pod is unable to start because the system has repeatedly tried and failed to pull the specified container image from a container registry.
- It occurs when kubernetes fails to pull the container image. (It might be wrong image name or tag).

## WrongImageName.yaml
```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx: wrong-tag
    ports:
    - containerPort: 80
```

## Apply
```bash
sudo kubectl apply -f WrongImageName.yaml
```

## Verify
```bash
sudo kubectl get pods #check status
sudo kubectl describe pod nginx #eventsection
```
