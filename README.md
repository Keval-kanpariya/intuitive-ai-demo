# Kubernetes Cluster Assignment

## Author
Keval Kanpariya  
DevOps Engineer  

---

## Project Summary

This repository contains a complete Kubernetes cluster implementation built using **kubeadm**, including application deployment, monitoring, RBAC configuration, and etcd backup strategy.

The cluster consists of:

- 1 Control Plane Node  
- 1 Worker Node  
- containerd as runtime  
- Calico CNI  
- NGINX application with Ingress  
- Monitoring stack (Prometheus + Grafana)  
- RBAC & namespace isolation  
- etcd snapshot and restore procedure (Tested Restore procedure)
- Bonus production-grade enhancements  

Each folder in this repository contains its own detailed README explaining configuration, reasoning, and validation steps.

---

## Repository Structure

- `cluster/` → Kubernetes cluster setup (kubeadm, CNI, node join)
- `app/` → Application deployment, service, ingress
- `monitoring/` → Prometheus & Grafana setup
- `rbac/` → Namespace isolation and access control
- `etcd/` → Backup and restore documentation
- `bonus/` → Advanced Kubernetes features (HPA, PDB, PV/PVC)
- `docs/` → Architecture & network diagrams
- `screenshots/` → Implementation evidence

---

## Assignment Coverage

✔ Cluster Setup  
✔ Networking Configuration  
✔ Application Deployment  
✔ Ingress Configuration  
✔ Monitoring Stack  
✔ RBAC Implementation  
✔ etcd Backup & Restore  
✔ Bonus Enhancements  

---

## Focus Areas

This implementation demonstrates:

- Structured infrastructure design  
- Kubernetes internals understanding  
- Monitoring & observability  
- Security best practices  
- Backup and recovery strategy  
- Professional documentation structure  

---

For detailed implementation steps, configuration files, and troubleshooting notes, please refer to the respective folder documentation.
