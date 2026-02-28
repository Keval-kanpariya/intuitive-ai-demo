# BONUS TASKS – Kubernetes Advanced Implementation

##  Overview

This folder contains implementation of advanced Kubernetes features:

- PersistentVolume using GCP External Disk (manually mounted)
- PodDisruptionBudget (PDB)
- Horizontal Pod Autoscaler (HPA)

All YAML manifests are stored separately in this folder.

---

# Setup PersistentVolume using GCP External Disk (Manual Mount)

## Objective
Attach a GCP persistent disk to a node manually and expose it to pods using PersistentVolume and PersistentVolumeClaim.

---

## Step 1 — Create Disk in GCP

```bash
gcloud compute disks create my-disk \
  --size=10GB \
  --zone=<Zone>
```

---

## 🔹 Step 2 — Attach Disk to Node

```bash
gcloud compute instances attach-disk <node-name> \
  --disk=my-disk \
  --zone=<Zone>
```

---

## 🔹 Step 3 — Format and Mount Disk on Node

SSH into node:

```bash
sudo lsblk
```

Format disk (only first time):

```bash
sudo mkfs.ext4 /dev/<disk-device>
```

Create mount directory:

```bash
sudo mkdir /mnt/gcp-disk
```

Mount disk:

```bash
sudo mount /dev/<disk-device> /mnt/gcp-disk
```

(Optional) Persist mount:

```bash
sudo nano /etc/fstab
```

Add:

```
/dev/<disk-device> /mnt/gcp-disk ext4 defaults 0 2
```

---

## 🔹 Step 4 — Apply Kubernetes Resources

```bash
kubectl apply -f persistent-volume.yaml
kubectl apply -f persistent-volume-claim.yaml
```

Verify:

```bash
kubectl get pv
kubectl get pvc
```

Check pod volume mount:

```bash
kubectl describe pod <pod-name>
```

---

# 2. Add PodDisruptionBudget (PDB)

## Objective
Ensure minimum pod availability during voluntary disruptions.

---

## Apply PDB

```bash
kubectl apply -f poddisruptionbudget.yaml
```

Verify:

```bash
kubectl get pdb
```

Test behavior:

```bash
kubectl drain <node-name> --ignore-daemonsets --delete-emptydir-data
```

PDB ensures minimum pods remain available.

---

# 3. Setup Horizontal Pod Autoscaler (HPA)

## Objective
Automatically scale application based on CPU usage.

---

## Ensure Metrics Server is Installed

```bash
kubectl get pods -n kube-system | grep metrics-server
```

If not installed:

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

---

## Apply HPA

```bash
kubectl apply -f hpa.yaml
```

Verify:

```bash
kubectl get hpa
```

Monitor scaling:

```bash
kubectl top pods
kubectl describe hpa <hpa-name>
```

---

# Validation Commands

```bash
kubectl get pv
kubectl get pvc
kubectl get pods -A
kubectl get pdb
kubectl get hpa
```

---
