
# Kubernetes Logs Buildkite Plugin

A [Buildkite plugin](https://buildkite.com/docs/pipelines/plugins) that fetches pods from the given label query with the status `CrashLoopBackoff` and creates a build annotation with the logs.

## Example

```yaml
steps:
- plugins:
    kubernetes-logs#v0.0.1:
      label_query: "release=production,component=web"
      namespace: default
```

## Configuration

### `label_query` (required)
The label query to use with `kubectl`. `kubectl get pods -l "<query>"`

### `namespace`
The Kuberentes namespace to look in. Defaults to `default`.
