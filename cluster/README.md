# Cluster Setup (kubeadm)

This directory documents the Kubernetes cluster bootstrap process.

## Architecture

- 1 Control Plane Node
- 1 Worker Node
- containerd as container runtime
- Calico as CNI plugin

## Key Steps

### 1. Disable swap
Kubernetes requires swap to be disabled for proper resource scheduling.

### 2. Install containerd
Configured with systemd cgroup driver.

### 3. Install kubeadm, kubelet, kubectl

### 4. Initialize control plane

```bash
kubeadm init --apiserver-advertise-address=<CONTROL_PLANE_IP> \
--pod-network-cidr=192.168.0.0/16
