# Kubernetes Node NotReady - How to Identify the Problem

When a node is in **NotReady** state, it means the control plane cannot properly communicate with the node or some critical components are failing.

---

## 1. Check Node Status

```bash
kubectl get nodes
kubectl describe node <node-name>
```

### Look for:
- Conditions (MemoryPressure, DiskPressure, PIDPressure)
- NetworkUnavailable
- Kubelet status

---

## 2. Check Kubelet Status

Kubelet is the most common reason for NotReady nodes.

```bash
systemctl status kubelet
journalctl -u kubelet -xe
```

### Possible Issues:
- Kubelet stopped/crashed
- Configuration errors
- Certificate expired

---

## 3. Check Node Resource Issues

### Memory / CPU Pressure

```bash
top
free -m
```

### Disk Pressure

```bash
df -h
```

If resources are exhausted:
- Node becomes NotReady
- Pods may get evicted

---

## 4. Check Container Runtime

If Docker / container runtime is down:

```bash
systemctl status docker
systemctl status containerd
```

### Fix:
- Restart the runtime
- Check logs

---

## 5. Check Network Issues

Node must communicate with control plane.

```bash
ping <master-node-ip>
curl -k https://<api-server>:6443
```

### Possible Issues:
- Firewall blocking
- Network plugin (CNI) failure

---

## 6. Check CNI Plugin

```bash
kubectl get pods -n kube-system
```

Look for:
- calico / flannel / weave pods not running

---

## 7. Check Disk & File System Issues

- Disk full
- File system corrupted

```bash
df -h
dmesg | grep -i error
```

---

## 8. Check Certificates

Kubelet certificates may expire.

```bash
ls -l /var/lib/kubelet/pki/
```

---

## 9. Check Node Conditions Summary

```bash
kubectl describe node <node-name>
```

Common Conditions:
- Ready = False
- MemoryPressure = True
- DiskPressure = True
- NetworkUnavailable = True

---

## 10. Quick Troubleshooting Steps

1. Restart kubelet:
```bash
systemctl restart kubelet
```

2. Restart container runtime:
```bash
systemctl restart docker
```

3. Free up disk space

4. Check network connectivity

---

## Interview Tip

**Short Answer:**
> "Node becomes NotReady due to kubelet failure, resource exhaustion, network issues, or container runtime problems. We troubleshoot using kubectl describe node, check kubelet logs, resources, and network connectivity."

