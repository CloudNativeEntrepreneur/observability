# Observability

## Install

Create the following resource in your argocd autopilot's `/projects` directory

### Helm + ArgoCD

```yaml
apiVersion: argoproj.io/v1alpha1
kind: AppProject
metadata:
  name: observability
  namespace: argocd
  annotations:
    argocd.argoproj.io/sync-wave: "2"
  finalizers:
    - resources-finalizer.argocd.argoproj.io
spec:
  description: Observability
  sourceRepos:
  - '*'
  destinations:
  - namespace: '*'
    server: https://kubernetes.default.svc
  clusterResourceWhitelist:
  - group: '*'
    kind: '*'
  namespaceResourceWhitelist:
  - group: '*'
    kind: '*'

---

apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: observability
  namespace: argocd
  annotations:
    argocd.argoproj.io/sync-wave: "3"
  finalizers:
    - resources-finalizer.argocd.argoproj.io
spec:
  project: observability
  source:
    repoURL: https://github.com/cloudnativeentrepreneur/observability.git
    targetRevision: HEAD
    path: helm
  destination:
    server: https://kubernetes.default.svc
    namespace: observability
  syncPolicy:
    automated:
      selfHeal: true
      prune: true

```

## Included

### kube-prometheus-stack

Includes:
* Prometheus
* Alertmanager

### loki-stack
### custom grafana dashboard example