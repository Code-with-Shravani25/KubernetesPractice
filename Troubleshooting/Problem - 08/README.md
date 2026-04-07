# Kubernetes Node NotReady - How to Identify the Problem

When a node shows **NotReady** status in Kubernetes, it means the control plane cannot communicate properly with the node or some components are failing.

---

## 1. Check Node Status
```bash
kubectl get nodes
kubectl describe node <node-name>
```

Look for:
- Conditions (MemoryPressure, DiskPressure, PIDPressure)
- Node status: NotReady
- Events at the bottom

---

## 2. Check Kubelet Status
Kubelet is the main agent on the node.

```bash
sudo systemctl status kubelet
sudo journalctl -u kubelet -f
```

Common issues:
- Kubelet stopped
- Configuration errors
- Certificate issues

---

## 3. Check Node Connectivity
Ensure the node can communicate with the control plane.

```bash
ping <master-node-ip>
curl -k https://<api-server>:6443
```

Possible problems:
- Network failure
- Firewall blocking ports
- DNS issues

---

## 4. Check Container Runtime
Verify if Docker / container runtime is running.

```bash
sudo systemctl status docker
# or
sudo systemctl status containerd
```

If runtime is down → node becomes NotReady

---

## 5. Check Resource Pressure
Node may be under pressure:

```bash
kubectl describe node <node-name>
```

Look for:
- MemoryPressure
- DiskPressure
- CPU starvation

---

## 6. Check Disk Space
```bash
df -h
```

If disk is full:
- Pods cannot be scheduled
- Node becomes NotReady

---

## 7. Check Node Conditions
```bash
kubectl get node <node-name> -o json | grep -i conditions -A 10
```

---

## 8. Check Certificates
Kubelet certificates may be expired.

```bash
ls /var/lib/kubelet/pki/
```

---

## 9. Check CNI (Networking)
Network plugin issues can cause NotReady.

```bash
kubectl get pods -n kube-system
```

Look for:
- calico / flannel / weave pods not running

---

## 10. Check Logs on Node
```bash
journalctl -xe
dmesg
```

---

## Common Root Causes

| Issue | Description |
|------|------------|
| Kubelet down | Node agent not running |
| Network issue | Node cannot reach API server |
| Disk full | No space left |
| Memory pressure | Node resources exhausted |
| Container runtime down | Docker/containerd stopped |
| CNI failure | Network plugin not working |
| Certificate expired | Authentication failure |

---

## Quick Troubleshooting Flow

1. Check node status → `kubectl get nodes`
2. Describe node → `kubectl describe node`
3. Check kubelet → `systemctl status kubelet`
4. Check runtime → `docker/containerd`
5. Check network → ping API server
6. Check disk/memory → `df -h`, `top`

---

## Interview Tip

**One-line answer:**
> "If a node is NotReady, I check kubelet, container runtime, network connectivity, resource pressure, and node events to identify the root cause."

