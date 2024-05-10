# Repository credential

Replace Repository credential in `sshPrivateKey: |`

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: argoproj-ssh-creds
  namespace: argocd
  labels:
    argocd.argoproj.io/secret-type: repo-creds
stringData:
  url: git@github.com:jumpbox-academy
  type: helm
  sshPrivateKey: |
    -----BEGIN OPENSSH PRIVATE KEY-----
    ... 
    -----END OPENSSH PRIVATE KEY-----
```

## How to create repository credential
```bash
ssh-keygen -t ed25519 -C "<key-name>"
```
**Output**
```bash
<key-name> <key-name>.pub
```

## How to use repository credential
1. use `<key-name>.pub` in github ssh `https://github.com --> Settings --> SSH and GPG keys --> New SSH key `
2. use `<key-name>` in `sshPrivateKey: |`
