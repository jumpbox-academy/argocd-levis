## How to config this plugins

Reference: https://argo-cd.readthedocs.io/en/stable/operator-manual/config-management-plugins/#config-management-plugins

**Parameter Setting**
- `name`: The name of the plugin must be unique within a given Argo CD instance.
- `version`:The version of your plugin. Optional. If specified, the Application's spec.source.plugin.name field

## When using the plugin
```yaml
  source:
    repoURL: git@github.com:<org>/<repo-name>
    targetRevision: <git-branch>
    path: <path>
    plugin:
      name: <plugin name>-<plugin version> e.g. <levis>-v1.7.0-beta
```