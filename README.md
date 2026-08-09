# homelab-cert-manager-config

cert-manager configuration for the homelab k3s cluster, managed via ArgoCD as its own Application — deliberately separate from [homelab-cert-manager](https://github.com/mattjmorrison/homelab-cert-manager) (the Helm chart install) and [homelab-cert-manager-crds](https://github.com/mattjmorrison/homelab-cert-manager-crds) (the CRDs).

Split out after discovering that using one git source both as a Helm `valueFiles` reference and a raw manifests `path` in the same ArgoCD Application caused stale renders — changes to these files weren't reliably picked up. This repo has a single-purpose source, avoiding that.

Contains:
- `secret-store.yaml` / `external-secret.yaml` — pulls `CLOUDFLARE_API_TOKEN` from OpenBao via External Secrets Operator
- `cluster-issuer-staging.yaml` / `cluster-issuer-prod.yaml` — Let's Encrypt via Cloudflare DNS-01
- `certificate.yaml` — the `*.morrisons.site` wildcard cert (currently issued via staging)
- `tlsstore.yaml` — installs that cert as Traefik's cluster-wide default

---

[Homelab Docs](https://github.com/mattjmorrison/homelab/blob/main/docs/INDEX.md)
