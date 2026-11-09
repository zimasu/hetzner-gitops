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

## How it works

This repo follows the **App of Apps** GitOps pattern.  
`root-application.yaml` registers every app in `apps/` with ArgoCD.  
ArgoCD continuously polls this repo and syncs any changes to the k3s cluster automatically.

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant GH as GitHub (this repo)
    participant ACD as ArgoCD
    participant K3S as k3s Cluster

    Dev->>GH: git push (update manifest)
    ACD->>GH: poll for changes
    ACD->>K3S: sync updated manifests
    K3S-->>ACD: report sync status
```
