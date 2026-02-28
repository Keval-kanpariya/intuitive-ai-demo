# RBAC & Namespace Isolation

This directory contains namespace isolation and RBAC configuration.

## Namespace

dev

## Components

- ServiceAccount: dev-sa
- Role: pod-reader
- RoleBinding

## Principle Applied

Least privilege access.

The Role allows:
- get
- list
- watch

Only for pods inside dev namespace.

## Verification

```bash
kubectl auth can-i list pods \
--as=system:serviceaccount:dev:dev-sa -n dev
