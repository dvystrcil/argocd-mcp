# argocd-mcp

K8s deploy manifests for `argocd-mcp` — an OWUI-reachable MCP tool server wrapping [`argoproj-labs/mcp-for-argocd`](https://github.com/argoproj-labs/mcp-for-argocd). Image built by the sibling repo [`dvystrcil/argocd-mcp-docker`](https://github.com/dvystrcil/argocd-mcp-docker). Three-repo split — see `architecture/owui-extensibility-mechanisms.md` in `dvystrcil/homelab`.

Tracked: `dvystrcil/homelab#815`.

## Layout

- `base/` — namespace, Deployment, Service, VPA (Off mode, D-012), Harbor pull secret (InfisicalSecret), ArgoCD token secret (InfisicalSecret)
- `overlays/` — flat D-015 shape, no per-environment split
- `image-updater/` — ImageUpdater CR tracking semver releases of the Harbor image

## Auth

`ARGOCD_BASE_URL`/`ARGOCD_API_TOKEN` are injected via the `argocd-mcp-secrets` InfisicalSecret, sourced from `ARGOCD_MCP_BASE_URL`/`ARGOCD_MCP_TOKEN` in Infisical. The token is minted from a **read-only** ArgoCD RBAC role (`role:readonly`, get/list only on `applications`/`logs`/`clusters`/`projects` — no `sync`/`create`/`update`/`delete`/`override`/`action`). See `dvystrcil/homelab#815` for the RBAC policy and live verification receipt.

## License

[MIT](LICENSE).
