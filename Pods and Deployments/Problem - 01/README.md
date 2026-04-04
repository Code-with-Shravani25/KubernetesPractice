# 🚀 Kubernetes Cluster Setup using Minikube (Ubuntu)

This guide explains how to set up a local Kubernetes cluster using **Minikube** with Docker as the driver on an Ubuntu system.

---

## 📌 Prerequisites

- Ubuntu system (20.04 or later recommended)
- sudo privileges
- Internet connection

---

## 🐳 Step 1: Install Docker

Update system packages:

```bash
sudo apt update -y
```

Install Docker:

```bash
sudo apt install docker.io -y
```

Verify Docker installation:

```bash
docker --version
```

(Optional) Enable and start Docker:

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

(Optional - Recommended) Run Docker without sudo:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## ☸️ Step 2: Install kubectl

Download the latest version of kubectl:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

Download checksum file:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```

Verify checksum (optional but recommended):

```bash
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

Install kubectl:

```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

Verify installation:

```bash
kubectl version --client
```

---

## ⚙️ Step 3: Install Minikube

Download Minikube:

```bash
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
```

Install Minikube:

```bash
sudo install minikube-linux-amd64 /usr/local/bin/minikube
rm minikube-linux-amd64
```

Verify installation:

```bash
minikube version
```

---

## ▶️ Step 4: Start Minikube Cluster

Start Minikube using Docker driver:

```bash
minikube start --driver=docker
```

If running as root (not recommended):

```bash
sudo minikube start --driver=docker --force
```

Check cluster status:

```bash
minikube status
```

---

## 🧪 Step 5: Verify Kubernetes Cluster

Check nodes:

```bash
kubectl get nodes
```

Check all pods:

```bash
kubectl get pods -A
```

---

## 🛠️ Useful Commands

| Command               | Description           |
|----------------------|----------------------|
| `minikube stop`      | Stop the cluster     |
| `minikube delete`    | Delete the cluster   |
| `minikube status`    | Check cluster status |
| `kubectl get all -A` | View all resources   |
| `kubectl get nodes`  | List cluster nodes   |

---

## ❗ Troubleshooting

### 1. Docker permission issue

**Error:**
```
Got permission denied while trying to connect to Docker daemon
```

**Fix:**
```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

### 2. Minikube fails to start

```bash
minikube delete
minikube start --driver=docker
```

---

### 3. kubectl not found

```bash
echo $PATH
```

---

## ⚠️ Notes

- `--driver=docker` runs Kubernetes inside Docker (lightweight setup)
- Avoid using `sudo` unless required
- Minikube is for learning and development, not production

---

## 🎯 Conclusion

You now have a fully functional local Kubernetes cluster using Minikube 🎉  

This setup is perfect for:

- Kubernetes practice  
- Interview preparation  
- Local development  

---

## 📚 References

- Kubernetes Docs: https://kubernetes.io/docs/
- Minikube Docs: https://minikube.sigs.k8s.io/docs/
