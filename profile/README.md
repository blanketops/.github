<div align="center">

<img src="https://avatars.githubusercontent.com/u/275803309?v=4" width="120" alt="BlanketOps logo" />

# BlanketOps

**Deterministic software delivery for Kubernetes.**

Entropy reduction through governed state progression.

[![Website](https://img.shields.io/badge/site-blanketopsenvironments.netlify.app-1f6feb)](https://blanketopsenvironments.netlify.app/)
[![CLI Release](https://img.shields.io/github/v/release/blanketops/environments-cli?label=environments-cli)](https://github.com/blanketops/environments-cli/releases/latest)
[![License](https://img.shields.io/badge/license-see%20repos-lightgrey)](https://github.com/blanketops)

</div>

---

## What it does

Two phases, one platform:

1. **BlanketOps Environments** — turns a `git push` into a running, TLS-terminated Kubernetes service. Nine typed, composable primitives (`Environment`, `GitRepository`, `GitHubEvent`, `Build`, `Package`, `Deployment`, `ServiceUnit`, `Route`, `Domain`), each owning one concern and reconciling toward a declared intent instead of a script that quietly patches around failures. If a stage can't legally proceed, it fails visibly. → [`environments-cli`](https://github.com/blanketops/environments-cli)
2. **Secure Software Supply Chain** — drives build → scan → sign → attest → publish on every push, via Tekton and Sigstore. Treats your pipeline as infrastructure, not a script. → [`secure-software-supplychain`](https://github.com/blanketops/secure-software-supplychain)

Setup and usage for each are covered in their own repo's README — that's the source of truth, not this page.

## Repositories

| Repo | What it is |
|---|---|
| [**environments-cli**](https://github.com/blanketops/environments-cli) | Zero-dependency, single-binary Kubernetes bootstrapper for BlanketOps Environments. No `kubectl` required. Built for air-gapped, bare-metal, and immutable environments. |
| [**environments-install**](https://github.com/blanketops/environments-install) | Declarative install manifests (CRDs, RBAC, controller-manager) as Kustomize overlays, published as a single `install.yaml` per release. |
| [**environments-api**](https://github.com/blanketops/environments-api) | The canonical Kubernetes API contracts (CRDs) for BlanketOps Environments. |
| [**environments-contract**](https://github.com/blanketops/environments-contract) | Canonical Go contracts shared across the platform's controllers and tooling. |
| [**secure-software-supplychain**](https://github.com/blanketops/secure-software-supplychain) | A Kubebuilder operator for the Secure Software Supply Chain phase — build → scan → sign → attest → publish, via Tekton and Sigstore. |

## Tech stack

- **Language:** Go
- **Runtime:** Kubernetes (CRDs, controllers, Kubebuilder)
- **CI/CD engine:** Tekton Pipelines + Triggers
- **Packaging & lifecycle:** Carvel `kapp-controller`
- **Eventing:** Argo Events
- **Builds:** Shipwright, Buildah
- **Serverless:** Knative Serving + Kourier
- **Infra orchestration:** Crossplane
- **Secrets:** External Secrets Operator
- **Supply chain security:** cosign, Sigstore (Fulcio/Rekor), Trivy, SLSA provenance attestation

## Links

- 🌐 Site: [blanketopsenvironments.netlify.app](https://blanketopsenvironments.netlify.app/)
- 📦 All repos: [github.com/orgs/blanketops/repositories](https://github.com/orgs/blanketops/repositories)

---

<div align="center">
<sub>Building predictable, entropy-reducing delivery for Kubernetes — one governed state transition at a time.</sub>
</div>
