# argocd-levis

## How to use levis plugin in Argocd >2.4 (current testing version: 2.11 on ArgoCD non HA)

**1. Installation Part**
```bash
kubectl apply -f 01_installation/01_install.yaml -f 01_installation/02_argocd-cmd-params-cm.yaml -n argocd
```

**Config insecure server via `argocd-cmd-params-cm.yaml` file**
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

**Incase using Ingress via Proen Cloud**

please sign domain dns 

**2. Install Plugin `without configmap way`**

skip this way when you use `with configmap way`

```bash
kubectl apply -f 01_installation/03_deployment-patch.yaml -n argocd
```

**2-2. Install Plugin `with configmap way`**

skip this way when you use `without configmap way`

```bash
kubectl apply -f 01_installation/03-2_deployment-patch-mount-cm -f 0X_custom_plugins -n argocd
```

**3. Install Ingress**
```bash
kubectl apply -f 01_installation/04_ingress.yaml -n argocd
```

**4. Install Git Repository Credential**

Please Generate Git Credential (SSH Private Key) and fill to `argocd-repo-creds.yaml` file before apply 

```bash
kubectl apply -f 02_repo-credential -n argocd
```

**5. Install Argo Application for monitoring app in `deployment` folder**

for default

```bash
kubectl apply -f 03_argo-app/k8s-default.yaml -n argocd
```

for levis

```bash
kubectl apply -f 03_argo-app/levis.yaml -n argocd
```

## NOTE: When to use Configmap (*2-2. Install Plugin `with configmap way`)
- you need to adjust plugin `version`
- you need optimize process of plugin `init`, `generate` and `others` in `kind: ConfigManagementPlugin`