# What Happens to Pods When a Node Goes Down in Kubernetes

When a node in a Kubernetes cluster goes down, several things happen to the pods running on that node. Below is a detailed explanation:

---

## 1. Node Becomes NotReady
- Kubernetes detects that the node is not responding.
- The node status changes to **NotReady**.

---

## 2. Pods Become Unavailable
- Pods running on that node stop functioning.
- They are marked as **Unknown** or **NotReady**.

---

## 3. Grace Period (Default ~5 minutes)
- Kubernetes waits for a default timeout (typically 5 minutes).
- This allows temporary network issues to recover.

---

## 4. Pods Are Marked for Deletion
- After the timeout, Kubernetes marks the pods on the failed node for deletion.

---

## 5. Controller Takes Action
Depending on the controller used:

### a. Deployment / ReplicaSet
- New pods are automatically created on healthy nodes.
- Maintains the desired replica count.

### b. StatefulSet
- Pods are recreated, but with stable identities.
- May take longer due to volume attachment.

### c. DaemonSet
- Pods will run only on available nodes.
- No replacement for the lost node until it recovers.

---

## 6. Rescheduling Pods
- Kubernetes scheduler assigns new pods to healthy nodes.
- Ensures cluster stability and availability.

---

## 7. Data Loss Consideration
- Pods using **ephemeral storage** lose data.
- Persistent volumes (PV) may reattach if supported.

---

## 8. Node Recovery Scenario
If the node comes back:
- It may rejoin the cluster.
- Old pods are not reused (new ones already created).

---

## Summary
- Node failure leads to pod failure.
- Kubernetes automatically recovers by rescheduling pods.
- High availability is maintained using controllers.

---

## Interview Tip
If asked in interviews:

**Answer in one line:**
> "When a node goes down, pods become unavailable, Kubernetes marks them for deletion, and controllers recreate them on healthy nodes."

