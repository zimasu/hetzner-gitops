![k3s](https://img.shields.io/badge/k3s-latest-blue)
![ArgoCD](https://img.shields.io/badge/ArgoCD-GitOps-orange)
![Helm](https://img.shields.io/badge/Helm-charts-blueviolet)
![Hetzner](https://img.shields.io/badge/Hetzner-Cloud-red)
# hetzner-gitops
K3s cluster running on Hetzner Cloud and managed with ArgoCD.
## Motivation
Managing self-hosted services manually became error-prone. This repo makes every deployment reproducible and auditable via Git.
## Structure
App-of-Apps: `root-application.yaml` syncs `apps/`.
Each file in `apps/` points ArgoCD at a path in `manifests/`.

    apps/       ArgoCD Application manifests
    manifests/  Kubernetes manifests per service
    charts/     Custom Helm charts (NocoDB, ARM64)

## Stack
- k3s
- ArgoCD
- ingress-nginx
- cert-manager
- Helm
- GitHub Actions

## Services
- Gitea
- n8n
- NocoDB
- Open WebUI
- ntfy
- Anki
- MkDocs
- BookStack
