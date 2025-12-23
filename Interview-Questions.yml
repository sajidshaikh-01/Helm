---

## 1. What problem does Helm solve in Kubernetes?

Helm solves the problem of **managing complex Kubernetes YAMLs** by providing:

* Reusable application packaging
* Environment‑specific configuration
* Versioning and rollback
* Easy upgrades

In production, Helm reduces manual errors and improves deployment consistency.

---

## 2. Helm vs kubectl apply – why do we need Helm?

* `kubectl apply` deploys raw YAML files
* Helm manages the **entire application lifecycle**

Helm supports:

* Install, upgrade, rollback
* Release history
* Parameterized deployments

---

## 3. What is a Helm Chart?

A Helm chart is a **packaged Kubernetes application** that contains:

* Kubernetes manifests (templates)
* Default configuration values
* Metadata and version info

---

## 4. What is a Helm Release?

A release is a **running instance of a Helm chart** in a Kubernetes cluster.

Each time you install or upgrade, Helm creates a **new release version**.

---

## 5. Difference between Chart.yaml and values.yaml?

* **Chart.yaml** → metadata (name, version, description)
* **values.yaml** → configurable values (image, replicas, ports)

---

## 6. How do you deploy the same app to dev, stage, and prod?

By using **separate values files**:

```bash
helm install myapp ./chart -f values-dev.yaml
helm install myapp ./chart -f values-prod.yaml
```

Same chart, different configurations.

---

## 7. How does Helm rollback work?

Helm stores **release history** inside the cluster.

Rollback command:

```bash
helm rollback myapp 1
```

This restores the application to a previous stable version.

---

## 8. What happens if a Helm upgrade fails in production?

If not handled properly, the deployment may be partial.

Best practice:

```bash
helm upgrade myapp ./chart --atomic
```

This automatically **rolls back** if the upgrade fails.

---

## 9. What is the difference between Helm v2 and Helm v3?

* Helm v2 used **Tiller** (security risk)
* Helm v3 removed Tiller and talks directly to the API server

Helm v3 is more secure and production‑ready.

---

## 10. What are Helm hooks?

Hooks allow running Kubernetes resources at specific lifecycle events.

Used for:

* Database migrations
* Pre‑install checks
* Cleanup tasks

---

## 11. How do you handle secrets in Helm?

❌ Do NOT store secrets in `values.yaml`

✅ Use:

* Kubernetes Secrets
* External Secrets
* HashiCorp Vault
* Sealed Secrets

---

## 12. What is `_helpers.tpl`?

It is used to define **reusable template logic**, such as:

* Common labels
* Resource names
* Annotations

Helps keep templates clean and DRY.

---

## 13. Helm vs Kustomize – what’s the difference?

* Helm → application lifecycle management
* Kustomize → YAML customization

Helm supports versioning and rollback, Kustomize does not.

---

## 14. What is `helm lint`?

It validates Helm charts for:

* Syntax errors
* Best practices
* Template issues

Used before deploying to production.

---

## 15. How do you test a Helm chart without deploying it?

```bash
helm template ./chart
```

This renders Kubernetes YAML locally.

---

## 16. How does Helm support zero‑downtime deployments?

Helm relies on Kubernetes **rolling update strategy**.

Pods are replaced gradually, ensuring application availability.

---

## 17. How are Helm dependencies managed?

Using `dependencies` in `Chart.yaml`.

Example use case:

* Application depends on MySQL or Redis

---

## 18. How is Helm used in CI/CD pipelines?

Helm is used in Jenkins / GitHub Actions / GitLab CI for deployments.

Typical command:

```bash
helm upgrade --install myapp ./chart -f values-prod.yaml --atomic
```

---

## 19. Can multiple Helm releases exist in the same cluster?

Yes.

Each release has a **unique name** and can run independently.

---



