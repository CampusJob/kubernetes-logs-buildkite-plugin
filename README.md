
# Kubernetes Logs Buildkite Plugin

A [Buildkite plugin](https://buildkite.com/docs/pipelines/plugins) that fetches pods from the given label query with the status `CrashLoopBackoff` and creates a build annotation with the logs.


## Configuration

A label query and namespace need to be set for `kubectl` to know which pods to query for. They can be set either with configuration parameters or dynamically in the `command` section, using the environmental variables `NAMESPACE` and `LABEL_QUERY`.

### `label_query`
The label query to use with `kubectl`. `kubectl get pods -l "<query>"`

### `namespace`
The Kubernetes namespace to look in. Defaults to `default`.


## Example

Configuration:
```yaml
steps:
- plugins:
    kubernetes-logs#v0.0.1:
      label_query: "release=production,component=web"
      namespace: default
```

Dynamic:
```yaml
steps:
- command: |
    export LABEL_QUERY="$(echo 'release=production')"
  plugins:
    kubernetes-logs#v0.0.1: {}
```