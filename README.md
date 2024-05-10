# argocd-levis

## Config insecure server via `argocd-cmd-params-cm.yaml`
```yaml
kind: ConfigMap
metadata:
  name: argocd-cmd-params-cm
  namespace: argocd
  labels:
    app.kubernetes.io/name: argocd-cmd-params-cm
    app.kubernetes.io/part-of: argocd
data:
  # Run server without TLS
  server.insecure: "true"
```

## Incase using Ingress via Proen Cloud
please sign domain dns 
