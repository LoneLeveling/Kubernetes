Kubernetes Architecture


<img width="457" height="466" alt="image" src="https://github.com/user-attachments/assets/3e15672f-d47f-44f6-ac99-a4af131fe4ba" />

🔵 Control Plane (Master)
### 1. API Server

- **Entry point to Kubernetes.**
- Receives requests from `kubectl`, users, and other components.
- Validates requests and updates cluster state in `etcd`.

> **Think:** Receptionist of the cluster.
> 

### 2. etcd

- **Key-value database** storing Kubernetes cluster state/configuration.
- Stores things like Pods, Deployments, Services, secrets/configuration metadata, etc.

> **Think:** Kubernetes' database/memory.
> 

### 3. Scheduler

- Decides **which Worker Node should run a newly created Pod**.
- Considers resources, constraints, affinity, taints/tolerations, etc.

> **Think:** Assigns Pods to suitable nodes.
> 

### 4. Controller Manager

- Runs various **controllers** that continuously compare desired state with actual state.
- Takes corrective action when they don't match.

Example:

```
Desired: 3 Pods
Actual:  2 Pods
        ↓
Controller creates another Pod
```

> **Think:** Keeps the cluster in the desired state.

# 🟢 Worker Node / Data Plane

### 1. Kubelet

- Agent running on **every Worker Node**.
- Communicates with the API Server.
- Ensures the Pods/containers assigned to its node are **running and healthy**.

> **Think:** Manager of Pods on that node.
> 

### 2. Container Runtime

- Actually **runs the containers**.
- Examples: **containerd, CRI-O**.
- Handles pulling images, creating, starting, stopping containers.

> **Think:** Engine that actually runs containers.
> 

### 3. kube-proxy

- Runs on each Worker Node.
- Handles **Kubernetes Service networking**.
- Helps route traffic from a Service to the appropriate backend Pods.

> **Think:** Traffic router for Services.

Summary:

<img width="390" height="294" alt="image" src="https://github.com/user-attachments/assets/12324ce6-10de-427b-ae92-932941006c50" />

**Control Plane components are**:

**API Server + etcd + Scheduler + Controller Manager**

And The standard **Worker/Data Plane components are**:

**kubelet + kube-proxy + container runtime**

→ Control plane = the one controlling the actions and the ‘Data’ Plane is the one executing the actions.

