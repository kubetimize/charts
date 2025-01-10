# Kubetimize Helm Charts

## Overview

This repository contains Helm charts for deploying Kubetimize components, including:

1. **Kubetimize Helm Chart**
2. **Kubetimize Backend Helm Chart**

Each chart is designed to simplify the deployment of Kubetimize on Kubernetes, with customizable variables for flexible configurations.

---

## Installation

### Prerequisites

- Kubernetes cluster (v1.20+ recommended)
- Helm v3 or higher
- Access to the appropriate container registry for Kubetimize images

### Installation Steps

#### 1. Add the Helm Repository

```bash
helm repo add kubetimize https://chart.kubetimize.io
helm repo update
```

#### 2. Install the Kubetimize Chart

```bash
helm install kubetimize kubetimize/kubetimize \
  --namespace kubetimize \
  --create-namespace \
  --values values.yaml
```

- Replace `values.yaml` with your custom values file (optional).

#### 3. Install the Kubetimize Backend Chart Separately (Optional)

If you need to deploy only the backend component:

```bash
helm install kubetimize-backend kubetimize/kubetimize-backend \
  --namespace kubetimize \
  --values backend-values.yaml
```

---

## Configuration

Each chart supports a variety of configuration options through the `values.yaml` file. Below is a detailed list of configurable variables for each chart.
### Kubetimize Helm Chart

| Parameter                        | Description                           | Default            |
| -------------------------------- | ------------------------------------- | ------------------ |
| `apiKey`                         | Generated API Key from account        | ``             |
| `backend.enabled`                | Deploy the backend component          | `true`             |
| `frontend.enabled`               | Deploy the frontend component         | `true`             |
| `global.imagePullSecrets`        | Image pull secrets for all components | `[]`               |
| `global.namespace`               | Namespace for all components          | `kubetimize`       |
| `backend.replicaCount`           | Number of replicas for backend        | `1`                |
| `frontend.replicaCount`          | Number of replicas for frontend       | `1`                |
| `ingress.enabled`                | Enable ingress for the application    | `false`            |
| `ingress.hosts[0].host`          | Hostname for the ingress              | `kubetimize.local` |
| `ingress.hosts[0].paths[0].path` | Path for the ingress                  | `/`                |
| `ingress.tls`                    | TLS configuration for ingress         | `[]`               |


### Kubetimize Backend Helm Chart

| Parameter                   | Description                          | Default              |
| --------------------------- | ------------------------------------ | -------------------- |
| `replicaCount`              | Number of replicas                   | `1`                  |
| `image.repository`          | Backend Docker image repository      | `kubetimize/backend` |
| `image.tag`                 | Backend Docker image tag             | `latest`             |
| `image.pullPolicy`          | Image pull policy                    | `IfNotPresent`       |
| `service.type`              | Service type                         | `ClusterIP`          |
| `service.port`              | Service port                         | `5000`               |
| `resources.requests.cpu`    | CPU requests for the container       | `250m`               |
| `resources.requests.memory` | Memory requests for the container    | `256Mi`              |
| `resources.limits.cpu`      | CPU limits for the container         | `500m`               |
| `resources.limits.memory`   | Memory limits for the container      | `512Mi`              |
| `nodeSelector`              | Node selector for scheduling         | `{}`                 |
| `tolerations`               | Tolerations for pod scheduling       | `[]`                 |
| `affinity`                  | Affinity settings for pod scheduling | `{}`                 |

---

## Upgrading

To upgrade the chart to a new version:

```bash
helm upgrade kubetimize kubetimize/kubetimize \
  --namespace kubetimize \
  --values values.yaml
```

For the backend chart:

```bash
helm upgrade kubetimize-backend kubetimize/kubetimize-backend \
  --namespace kubetimize \
  --values backend-values.yaml
```

---

## Uninstalling

To uninstall the charts:

#### Uninstall the Parent Chart

```bash
helm uninstall kubetimize -n kubetimize
```

#### Uninstall the Backend Chart

```bash
helm uninstall kubetimize-backend -n kubetimize
```

---

## Support

For further assistance, please reach out to the Kubetimize support team or visit the documentation site.

