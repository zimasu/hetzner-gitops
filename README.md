# hetzner-gitops
K3s cluster running on Hetzner Cloud and managed with ArgoCD.
## Motivation
SSH is stateless. Every session starts from scratch, which makes it hard to audit and maintain.
## Solution
This repo is stateful which means it acts as a single source of truth.
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
