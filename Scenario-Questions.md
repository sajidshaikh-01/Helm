# Helm Mock Interview – Real Interviewer Style Q&A (DevOps)
---

## Interview Round Style

* Interviewer asks short, open-ended questions
* Expects **production examples**, not definitions
* Follow-up questions test depth

---

## Q1. What is Helm and why do we need it when we already have Kubernetes YAML?

**Expected Answer:**
Helm is a package manager for Kubernetes that helps manage applications using reusable charts. While Kubernetes YAML can deploy resources, Helm adds **templating, versioning, rollback, and environment-specific configuration**, which is critical in production.

**Follow-up:** Why not just use kubectl apply?

**Good Answer:**
`kubectl apply` works for simple setups, but Helm manages the **full application lifecycle**, including upgrades and rollbacks, which kubectl cannot handle easily.

---

## Q2. What is a Helm chart and what does it contain?

**Expected Answer:**
A Helm chart is a packaged Kubernetes application. It contains metadata (`Chart.yaml`), default configuration (`values.yaml`), and Kubernetes manifests inside the `templates/` directory.

**Follow-up:** What happens if values are not provided?

**Good Answer:**
Helm uses values from `values.yaml` as defaults.

---

## Q3. Explain Helm chart structure from memory.

**Expected Answer:**

```text
Chart.yaml
values.yaml
templates/
_helpers.tpl
charts/
```

**Interviewer Tip:** If you remember `_helpers.tpl`, it shows real usage.

---

## Q4. How do you deploy the same application to dev, stage, and prod?

**Expected Answer:**
We use a single Helm chart with **separate values files** for each environment.

```bash
helm upgrade --install myapp ./chart -f values-dev.yaml
helm upgrade --install myapp ./chart -f values-prod.yaml
```

---

## Q5. What happens internally when you run `helm install`?

**Expected Answer:**
Helm renders templates using values, generates Kubernetes manifests, and sends them to the Kubernetes API server. The release metadata is stored in the cluster.

---

## Q6. How does Helm upgrade work in production?

**Expected Answer:**
Helm upgrades modify existing Kubernetes resources using rolling updates. Each upgrade creates a new release revision.

**Follow-up:** What if upgrade fails?

**Good Answer:**
We use `--atomic` so Helm automatically rolls back.

---

## Q7. How do you rollback a failed deployment?

**Expected Answer:**

```bash
helm rollback myapp 2
```

Helm restores the previous stable release.

---

## Q8. Where does Helm store release information?

**Expected Answer:**
Helm v3 stores release information as Kubernetes Secrets inside the cluster.

---

## Q9. Difference between Helm v2 and Helm v3?

**Expected Answer:**
Helm v2 used Tiller, which had security issues. Helm v3 removed Tiller and communicates directly with the API server.

---

## Q10. How do you manage secrets when using Helm?

**Expected Answer:**
We do not store secrets in values.yaml. We use Kubernetes Secrets, External Secrets, or Vault, and reference them in Helm templates.

---

## Q11. What are Helm hooks and where have you used them?

**Expected Answer:**
Helm hooks allow running tasks at specific lifecycle stages, such as pre-install or post-upgrade. They are commonly used for database migrations.

---

## Q12. How do you test Helm charts before deploying to production?

**Expected Answer:**

```bash
helm lint
helm template
```

This helps catch errors before deployment.

---

## Q13. Helm vs Kustomize – which one do you use and why?

**Expected Answer:**
Helm is used for application lifecycle management, while Kustomize is used for YAML customization. In production, Helm is preferred for versioning and rollback.

---

## Q14. How is Helm used in CI/CD pipelines?

**Expected Answer:**
Helm is used in Jenkins or GitHub Actions to deploy applications automatically after image build and push.

```bash
helm upgrade --install myapp ./chart --atomic
```

---

## Q15. How do you ensure zero downtime with Helm?

**Expected Answer:**
Helm relies on Kubernetes rolling update strategy and readiness probes to ensure traffic is only sent to healthy pods.

---

## Q16. Can multiple Helm releases run in the same cluster?

**Expected Answer:**
Yes, as long as each release has a unique name.

---

## Q17. What is `_helpers.tpl` and why is it important?

**Expected Answer:**
It contains reusable template logic for labels, names, and annotations, making charts cleaner and reusable.

---

## Q18. What are common mistakes people make with Helm?

**Expected Answer:**

* Storing secrets in values.yaml
* Not using atomic upgrades
* Hardcoding environment values
* Manual production deployments

---

## Q19. How would you explain Helm to a fresher?

**Expected Answer:**
Helm is like apt or yum for Kubernetes applications.

---

## Q20. How do you rate yourself in Helm?

**Best Answer:**

> I would rate myself 6–7/10. I’m confident in writing Helm charts, managing values, handling upgrades and rollbacks, and using Helm in CI/CD pipelines.

---
