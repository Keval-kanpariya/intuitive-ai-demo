## Kubernetes Cluster Assignment

## Overview

You are required to:

- Deploy a Kubernetes cluster with:
  - 1 Control Plane Node
  - 1 Worker Node
- Configure networking
- Deploy an application
- Implement monitoring (Prometheus + Grafana)
- Configure RBAC
- Perform etcd backup
- Document everything clearly

You must use **kubeadm** for cluster setup.

You must submit your work via Pull Request before the deadline.


##  TASK 1 – Cluster Setup

## Requirements

- Install container runtime (containerd recommended)
- Disable swap
- Install kubeadm, kubelet, kubectl
- Initialize control plane
- Join worker node
- Install CNI (Calico recommended)


##  TASK 2 – Application Deployment

Deploy a sample application (nginx or similar).

## Requirements

- Deployment with at least 2 replicas
- Service (NodePort)
- Liveness probe
- Readiness probe
- Resource requests and limits


##  TASK 3 – Ingress (Recommended)

Install NGINX Ingress Controller.

## Requirements

- Create Ingress resource
- Host-based routing

## Expected Result

Application accessible via:
```
http://myapp.local
```
---

#  TASK 4 – Monitoring Setup

Install monitoring stack using Helm.

Recommended:
- kube-prometheus-stack

Must include:

- Prometheus
- Grafana
- Node Exporter
- kube-state-metrics

## Expected Result

Grafana dashboards showing:

- Node CPU usage
- Node memory usage
- Pod CPU & memory usage
- Running pods count
- Node health status



#  TASK 5 – RBAC & Namespace Isolation

## Requirements

1. Create namespace:
   ```
   dev
   ```

2. Create:
   - ServiceAccount
   - Role (read-only pods)
   - RoleBinding


# TASK 6 – etcd Backup & Restore

## Requirements

- Take etcd snapshot
- Document restore steps

## Expected Result

- Snapshot file created
- Restore steps documented clearly

#  TASK 7 – Documentation (Very Important)

Your repository must include:

- Architecture diagram
- Network diagram
- Installation steps
- Configuration YAML files
- Helm values files (if used)
- Troubleshooting notes
- Screenshots of:
  - kubectl get nodes
  - kubectl get pods
  - Grafana dashboard
  - Working application

Documentation clarity will heavily impact evaluation.


# Submission Guidelines

1. Fork this repository
2. Create a new branch:
   ```
   submission-<your-name>
   ```
3. Push:
   - All YAML files
   - Helm configurations
   - Diagrams
   - Documentation
4. Create a Pull Request

Your commit history should reflect structured work (not one large commit).


Bonus Challenges (Optional but Strongly Recommended)

- Configure NetworkPolicy
- Setup Horizontal Pod Autoscaler
- Configure AlertManager
- Setup PersistentVolume using NFS
- Simulate worker node failure
- Add PodDisruptionBudget
- Configure certificate rotation


# Final Presentation

You will present:

- Architecture overview (10–15 minutes)
- Live demo
- Monitoring walkthrough
- Debugging explanation

#  Important Note

This assignment is not about memorizing commands.

We are evaluating:

- How you think
- How you debug
- How you structure infrastructure
- How deeply you understand Kubernetes internals
- How professionally you document your work


Good luck 
