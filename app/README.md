# Application Deployment

This directory contains application-related Kubernetes resources.

## Components

- Deployment (nginx)
- Service (NodePort)
- Ingress
- Probes and resource limits

## Deployment Design

- 2 replicas minimum
- CPU and memory requests defined for scheduling
- Limits defined for enforcement
- Liveness probe to restart unhealthy containers
- Readiness probe to prevent traffic to unready pods

## Service

NodePort used to expose service externally.

## Apply

```bash
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml
kubectl apply -f nginx-ingress.yaml
