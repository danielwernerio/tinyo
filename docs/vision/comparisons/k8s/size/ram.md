# K8s

## RAM Usage Analysis

### Memory Requirements for Minimal HA Setup

This document estimates the RAM (memory) usage of Kubernetes components in a minimal High Availability (HA) setup. It includes the memory requirements for control plane nodes, worker nodes, and shared tools, and it calculates the total memory footprint for the entire cluster.

---

## Key Kubernetes Components

### Control Plane Node
1. **kube-apiserver**
   - Memory usage: **~512 MB**
2. **kube-controller-manager**
   - Memory usage: **~200 MB**
3. **kube-scheduler**
   - Memory usage: **~100 MB**
4. **etcd**
   - Memory usage: **~256 MB** (varies with cluster size)

**Total Control Plane Components RAM Usage**: **~1,068 MB (~1.1 GB)**

---

### Worker Node
1. **kubelet**
   - Memory usage: **~512 MB**
2. **kube-proxy**
   - Memory usage: **~64 MB**

**Total Worker Node Components RAM Usage**: **~576 MB (~0.6 GB)**

---

## Shared Components Across All Nodes
1. **Container Runtime (e.g., containerd or CRI-O)**
   - Memory usage: **~128 MB**
2. **Networking Plugin (e.g., Calico, Flannel)**
   - Memory usage: **~64 MB**
3. **Additional Tools (e.g., kubectl, Helm)**
   - Memory usage: **~32 MB**

**Total Shared Components RAM Usage per Node**: **~224 MB (~0.2 GB)**

---

## Total RAM Estimation

### Per Node
1. **Control Plane Node**:
   - Kubernetes components: **~1,068 MB**
   - Shared components: **~224 MB**
   - **Total: ~1,292 MB (~1.3 GB)**

2. **Worker Node**:
   - Kubernetes components: **~576 MB**
   - Shared components: **~224 MB**
   - **Total: ~800 MB (~0.8 GB)**

### HA Setup (3 Control Plane + 2 Worker Nodes)
- **Control Plane Nodes (3 × 1,292 MB)**: **3,876 MB (~3.9 GB)**
- **Worker Nodes (2 × 800 MB)**: **1,600 MB (~1.6 GB)**

**Total RAM for HA Setup**: **~5,476 MB (~5.5 GB)**

---

## Notes
- These estimates cover the memory usage of Kubernetes components only. Additional memory will be needed for application workloads, monitoring tools, and logging systems.
- Recommended memory for nodes is typically higher to provide headroom for operational stability:
  - Control Plane Node: 2 GB
  - Worker Node: 1 GB
- Real-world memory usage may vary depending on cluster size, workloads, and configuration settings.