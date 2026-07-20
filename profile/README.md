<div align="center">

<img src="https://avatars.githubusercontent.com/u/275803309?v=4" width="120" alt="BlanketOps logo" />

# BlanketOps

**Deterministic software delivery for Kubernetes.**

Treat deployment as governed state progression, not a pipeline you hope doesn't drift.

[![Website](https://img.shields.io/badge/site-blanketopsenvironments.netlify.app-1f6feb)](https://blanketopsenvironments.netlify.app/)
[![CLI Release](https://img.shields.io/github/v/release/blanketops/environments-cli?label=environments-cli)](https://github.com/blanketops/environments-cli/releases/latest)
[![License](https://img.shields.io/badge/license-see%20repos-lightgrey)](https://github.com/blanketops)

</div>

---

## What we're building

Kubernetes delivery tooling accumulates entropy: pipelines quietly patch around failures, stages get skipped, and "it deployed" stops meaning "it's in the state you asked for." Teams stitch together CI systems that don't know about deployments, ingress configs that don't know about certs, workload runners that don't know about environments.

**BlanketOps Environments** fixes this by defining delivery as a set of composable, typed domain primitives — each owning a single concern, each reconciling toward a declared intent — instead of a pipeline:

| Primitive | Responsibility |
|---|---|
| `Environment` | Root of the delivery chain; secret-store authority |
| `GitRepository` | Source binding; commit SHA resolution |
| `GitHubEvent` | Webhook-driven trigger pipeline |
| `Build` | Image build lifecycle; BuildRun orchestration |
| `Package` | Artifact promotion and supply chain attestation |
| `Deployment` | Workload rollout; ServiceUnit lifecycle |
| `ServiceUnit` | Single workload declaration (image, port, size) |
| `Route` | Workload-to-host binding; runtime materialisation |
| `Domain` | TLS chain ownership; cert-manager + Knative bridge |

If a stage can't legally proceed, it **fails visibly** instead of being silently coerced into a "working" state. The result: code goes from IDE to production in minutes, with the drift and guesswork engineered out.

## Repositories

| Repo | What it is |
|---|---|
| [**environments-cli**](https://github.com/blanketops/environments-cli) | Zero-dependency, single-binary Kubernetes bootstrapper. Installs the full BlanketOps platform stack straight through the Kubernetes API — no `kubectl` required. Built for air-gapped, bare-metal, and immutable environments. |
| [**environments-install**](https://github.com/blanketops/environments-install) | Declarative install manifests (CRDs, RBAC, controller-manager) as Kustomize overlays, published as a single `install.yaml` per release. |
| [**environments-api**](https://github.com/blanketops/environments-api) | The canonical Kubernetes API contracts (CRDs) for BlanketOps Environments. |
| [**environments-contract**](https://github.com/blanketops/environments-contract) | Canonical Go contracts shared across the platform's controllers and tooling. |
| [**secure-software-supplychain**](https://github.com/blanketops/secure-software-supplychain) | A Kubebuilder operator that drives build → scan → sign → attest → publish on every push, via Tekton and Sigstore. *"Treat your pipeline as infrastructure, not a script."* |

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

Every CLI release ships **signed** (`cosign`, keyless) with a **SLSA-compliant provenance attestation** — verifiable via `cosign verify-blob` or `gh attest verify`.

## Getting started

```bash
curl -LO https://github.com/blanketops/environments-cli/releases/latest/download/bops-env-static
chmod +x bops-env-static
sudo mv bops-env-static /usr/local/bin/bops-env

bops-env install     # installs the operator + platform stack onto your cluster
bops-env version
```

Full docs and verification steps: see [environments-cli](https://github.com/blanketops/environments-cli#-provenance-signing--security).

## Links

- 🌐 Site: [blanketopsenvironments.netlify.app](https://blanketopsenvironments.netlify.app/)
- 📦 All repos: [github.com/orgs/blanketops/repositories](https://github.com/orgs/blanketops/repositories)

---

<div align="center">
<sub>Building predictable, entropy-reducing delivery for Kubernetes — one governed state transition at a time.</sub>
</div>
