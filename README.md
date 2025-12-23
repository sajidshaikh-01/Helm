# Helm – Complete Interview & Production Notes (DevOps)
---
## 1. What is Helm?

Helm is the **package manager for Kubernetes**. It helps you define, install, upgrade, and rollback Kubernetes applications using reusable packages called **Helm Charts**.

### Why Helm is needed

* Avoid duplicate YAML files
* Manage multiple environments (dev, stage, prod)
* Version control Kubernetes deployments
* Easy rollback during failures
* Simplifies CI/CD deployments

---

## 2. Helm Architecture (Helm v3)

* **Helm CLI** – runs on your machine or CI/CD runner
* **Kubernetes API Server** – Helm talks directly to it
* **Chart** – application package
* **Release** – running instance of a chart

⚠️ Helm v3 **does NOT use Tiller** (removed for security reasons).

---

## 3. Helm Chart Structure (Must Remember)

```text
myapp/
├── Chart.yaml        # Metadata about the chart
├── values.yaml       # Default configuration values
├── templates/        # Kubernetes manifest templates
│   ├── deployment.yaml
│   ├── service.yaml
│   └── _helpers.tpl
└── charts/           # Chart dependencies (sub-charts)
```

### Important files

* **Chart.yaml** → name, version, appVersion
* **values.yaml** → configurable values
* **templates/** → Kubernetes YAML with Go templating
* **_helpers.tpl** → reusable template logic

---

## 4. Helm Templating Basics (Very Important)

Helm uses **Go templates**.

Common built-in objects:

```yaml
{{ .Values.replicaCount }}
{{ .Release.Name }}
{{ .Chart.Name }}
{{ .Values.image.tag }}
```

### Example (Deployment snippet)

```yaml
replicas: {{ .Values.replicaCount }}
image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
```

---

## 5. Values Management (Dev / Stage / Prod)

One chart → multiple environments

```bash
helm install myapp ./chart -f values-dev.yaml
helm install myapp ./chart -f values-prod.yaml
```

Override using CLI:

```bash
helm upgrade myapp ./chart --set replicaCount=3
```

---

## 6. Helm Release Lifecycle

Important commands (interview MUST):

```bash
helm install
helm upgrade
helm rollback
helm uninstall
helm list
helm history
```

Rollback example:

```bash
helm rollback myapp 1
```

Helm stores **release history** in the cluster.

---

## 7. Helm Upgrade & Rollback in Production

### Atomic upgrade (Best Practice)

```bash
helm upgrade myapp ./chart --atomic
```

If upgrade fails → Helm **automatically rolls back**.

Helm relies on Kubernetes **rolling update strategy**, so zero-downtime is possible.

---

## 8. Helm Hooks

Hooks allow running Kubernetes resources at specific lifecycle events.

Common use cases:

* Database migrations
* Pre-install checks
* Cleanup jobs

Hook types:

* pre-install
* post-install
* pre-upgrade
* post-upgrade

Example annotation:

```yaml
annotations:
  helm.sh/hook: pre-install
```

---

## 9. Helm Dependencies (Subcharts)

Used when your app depends on other services (MySQL, Redis, etc.).

Chart.yaml example:

```yaml
dependencies:
- name: mysql
  version: 9.4.0
```

Install dependencies:

```bash
helm dependency update
```

---

## 10. Helm vs Kustomize (Interview Favorite)

| Helm            | Kustomize            |
| --------------- | -------------------- |
| Package manager | Config customization |
| Templating      | Overlay based        |
| Release history | No release tracking  |
| Rollbacks       | No rollback          |

Simple answer:

> Helm is for **application lifecycle**, Kustomize is for **YAML customization**.

---

## 11. Helm in CI/CD Pipelines

Used in:

* Jenkins
* GitHub Actions
* GitLab CI

Typical pipeline flow:

1. Build Docker image
2. Push to registry (ECR)
3. Update Helm values
4. Deploy using Helm

```bash
helm upgrade --install myapp ./chart -f values-prod.yaml --atomic
```

---

## 12. Helm on EKS (Production Flow)

1. Create EKS cluster (Terraform / eksctl)
2. Configure kubeconfig
3. Prepare Helm chart
4. Deploy via CI/CD
5. Use Ingress / ALB Controller
6. Monitor & rollback if needed

---

## 13. Secrets Management with Helm

❌ Do NOT store secrets in values.yaml

✅ Use:

* Kubernetes Secrets
* External Secrets
* HashiCorp Vault
* Sealed Secrets

---

## 14. Helm Best Practices (Must Say in Interview)

* One chart, multiple environments
* Separate values files per env
* Use `--atomic` for production
* Run `helm lint` before deploy
* Use `helm template` for dry run
* Do deployments via CI/CD, not manually

---

## 15. Common Helm Interview Questions (Short Answers)

* **What is a Helm chart?**
  → Packaged Kubernetes application

* **What is a release?**
  → Running instance of a chart

* **Helm v2 vs v3?**
  → Tiller removed in v3

* **How do you rollback?**
  → `helm rollback <release> <revision>`

* **Rate yourself in Helm?**
  → 6–7/10 (production confident)

---

## 16. Final Interview Summary (Say This)

> “We use Helm in production to package Kubernetes applications, manage environment-specific configurations using values files, deploy via CI/CD pipelines, and safely handle upgrades and rollbacks using Helm release history.”

---

