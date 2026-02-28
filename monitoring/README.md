# Monitoring Stack

Monitoring installed using Helm and kube-prometheus-stack.

## Components

- Prometheus
- Grafana
- Node Exporter
- kube-state-metrics
- AlertManager

## Installation

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install monitoring prometheus-community/kube-prometheus-stack \
--namespace monitoring
