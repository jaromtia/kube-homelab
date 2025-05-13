# Kubernetes Homelab with GitOps

This repository contains the configuration for a GitOps-managed Kubernetes homelab setup. The infrastructure is managed using ArgoCD for GitOps, with various components for monitoring, logging, and application deployment.

## Components

- **Kubernetes Cluster**: Managed using k3s for lightweight operation
- **GitOps**: ArgoCD for continuous deployment
- **Monitoring**: Prometheus + Grafana
- **Logging**: Loki + Promtail
- **Reverse Proxy**: Traefik
- **Networking**: Tailscale for secure remote access
- **CI/CD**: GitHub Actions for CI, ArgoCD for CD
- **Storage**: Longhorn for persistent storage

## Prerequisites

- A Linux server or VM with at least 4GB RAM and 2 CPU cores
- Tailscale account
- GitHub account
- Domain name (optional, for external access)

## Quick Start

1. Install k3s:
```bash
curl -sfL https://get.k3s.io | sh -
```

2. Install ArgoCD:
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

3. Apply the base configuration:
```bash
kubectl apply -f k8s/base/
```

4. Access ArgoCD:
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

## Directory Structure

```
.
├── k8s/                    # Kubernetes manifests
│   ├── base/              # Base configurations
│   └── overlays/          # Environment-specific overlays
├── apps/                  # Application configurations
│   ├── monitoring/        # Prometheus + Grafana
│   ├── logging/          # Loki + Promtail
│   ├── networking/       # Traefik + Tailscale
│   └── storage/          # Longhorn
└── ci/                   # CI/CD configurations
```

## Adding New Applications

To add new applications:

1. Create a new directory under `apps/` for your application
2. Create Kubernetes manifests or Helm values
3. Add an ArgoCD Application manifest in `k8s/base/`
4. Commit and push changes

## Maintenance

- Regular backups of persistent volumes
- Monitoring alerts for cluster health
- Regular updates of components

## Security Notes

- All sensitive data is stored in Kubernetes secrets
- Tailscale provides secure remote access
- Regular security updates are applied through GitOps

## License

MIT 