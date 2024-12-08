# K8s

## Binary Size Analysis

### Disk Space for Minimal HA Setup

This document aims to provide an accurate estimation of the total binary size and disk space required by Kubernetes components in a minimal High Availability (HA) setup. This estimation is based on the size of all key components and includes necessary supporting tools, but excludes storage for logs and application workloads.

---

## Key Kubernetes Components

### Control Plane Node
1. **kube-apiserver**
   - Binary size: **~50 MB**
   - Config and logs: **~10 MB**
   - **Total: ~60 MB**

2. **kube-controller-manager**
   - Binary size: **~40 MB**
   - Config and logs: **~5 MB**
   - **Total: ~45 MB**

3. **kube-scheduler**
   - Binary size: **~30 MB**
   - Config and logs: **~5 MB**
   - **Total: ~35 MB**

4. **etcd**
   - Binary size: **~20 MB**
   - Data storage: **~100 MB** (dependent on cluster size)
   - **Total: ~120 MB**

### Worker Node
1. **kubelet**
   - Binary size: **~100 MB**
   - Config and logs: **~10 MB**
   - **Total: ~110 MB**

2. **kube-proxy**
   - Binary size: **~40 MB**
   - Config and logs: **~5 MB**
   - **Total: ~45 MB**

---

## Shared Components Across All Nodes
1. **Container Runtime (e.g., containerd or CRI-O)**
   - Binary size: **~50 MB**
   - Space for container images: **~200 MB**
   - **Total: ~250 MB**

2. **Networking Plugin (e.g., Calico, Flannel)**
   - Plugin size: **~50 MB**
   - **Total: ~50 MB**

3. **Additional Tools**
   - kubectl size: 20 MB
   - helm, .. size: 10 MB
   - **Total: ~30 MB**

---

## Total Disk Space Estimation

### Per Node
1. **Control Plane Node**:
   - Kubernetes components: **~260 MB**
   - Shared components: **~330 MB**
   - **Total: ~600 MB**

2. **Worker Node**:
   - Kubernetes components: **~155 MB**
   - Shared components: **~330 MB**
   - **Total: ~485 MB**

### HA Setup (3 Control Plane + 2 Worker Nodes)
- **Control Plane Nodes (3 × 600 MB)**: **1,800 MB**
- **Worker Nodes (2 × 485 MB)**: **970 MB**

**Total Size for HA Setup**: **~2,770 MB (~2.8 GB)**

---

## Notes
- This analysis excludes storage needed for application workloads, logs, or other operational data.
- The recommended 40 GB per node is for the entire operating system, Kubernetes components, logs, and a buffer for future workloads. The actual binary size of Kubernetes totals a few gigabytes for an HA setup.
