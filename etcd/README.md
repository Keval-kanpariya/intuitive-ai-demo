# 🚀 ETCD Backup & Restore Procedure (Kubernetes Control Plane)

## 📌 Purpose

This document explains how to:

- Take an etcd snapshot (backup)
- Verify snapshot integrity
- Store the backup safely
- Restore etcd from snapshot (Disaster Recovery)

---

# 🧯 ETCD Backup Procedure

## 🔹 Step 1 — Take etcd Snapshot

Run on the **control plane node**:

```bash
sudo ETCDCTL_API=3 etcdctl snapshot save snapshot.db \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key
```

If `etcdctl` is not installed:

```bash
sudo apt install etcd-client -y
```

---

## 🔹 Step 2 — Verify Snapshot

Check snapshot file:

```bash
ls -lh snapshot.db
```

File size should be greater than a few MB.

Validate snapshot:

```bash
ETCDCTL_API=3 etcdctl snapshot status snapshot.db --write-out=table
```

Expected output format:

```
+----------+----------+------------+------------+
| HASH     | REVISION | TOTAL KEYS | TOTAL SIZE |
+----------+----------+------------+------------+
```

✅ This confirms the snapshot is valid.

---

## 🔹 Step 3 — Move Snapshot to Safe Location

```bash
sudo mkdir -p /backup
sudo mv snapshot.db /backup/
```

Recommended (Production):
- Store backup outside the node
- Upload to S3 or external storage

---

# 🔁 ETCD Restore Procedure (Disaster Recovery)

⚠️ Do NOT perform restore on production unless required.

---

## 🔹 Step 1 — Stop kubelet

```bash
sudo systemctl stop kubelet
```

---

## 🔹 Step 2 — Backup Existing etcd Data

Check current data directory:

```bash
sudo cat /etc/kubernetes/manifests/etcd.yaml | grep data-dir
```

Usually:

```
/var/lib/etcd
```

Backup existing data:

```bash
sudo mv /var/lib/etcd /var/lib/etcd-backup
```

---

## 🔹 Step 3 — Restore Snapshot

```bash
sudo ETCDCTL_API=3 etcdctl snapshot restore /backup/snapshot.db \
  --data-dir=/var/lib/etcd \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key
```

---

## 🔹 Step 4 — Verify etcd Manifest

Open etcd static pod manifest:

```bash
sudo nano /etc/kubernetes/manifests/etcd.yaml
```

Ensure the following matches:

```
--data-dir=/var/lib/etcd
```

Update if necessary.

---

## 🔹 Step 5 — Start kubelet

```bash
sudo systemctl start kubelet
```

Kubelet will automatically restart the etcd static pod.

---

## 🔹 Step 6 — Verify Cluster Recovery

```bash
kubectl get nodes
kubectl get pods -A
```

Cluster should return to healthy state.

---

# 🛡 Best Practices

- Schedule regular etcd backups (cron job)
- Store backups externally (S3/NFS/backup server)
- Test restore in staging environment
- Monitor etcd disk usage
- Protect backup files securely

---

# 📌 Summary

| Task | Command |
|------|----------|
| Take Backup | `etcdctl snapshot save` |
| Verify Backup | `etcdctl snapshot status` |
| Restore Backup | `etcdctl snapshot restore` |
| Restart Cluster | `systemctl restart kubelet` |

---
