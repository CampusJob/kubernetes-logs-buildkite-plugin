
# Kubernetes Logs Buildkite Plugin

A [Buildkite plugin](https://buildkite.com/docs/pipelines/plugins) that fetches pods from the given label query with the status `CrashLoopBackoff` and creates a build annotation with the logs.


## Configuration

A label query and namespace need to be set for `kubectl` to know which pods to query for. They can be set either with configuration parameters or dynamically using [Buildkite metadata](https://buildkite.com/docs/agent/v3/cli-meta-data), with the metadata keys `KUBERNETES_LOGS_LABEL_QUERY` and `KUBERNETES_LOGS_NAMESPACE`.

### `label_query`
The label query to use with `kubectl`, as in `kubectl get pods -l "<query>"`.
A label query **must** be provided.

### `namespace`
The Kubernetes namespace to look in. Defaults to `default`.


## Example

Configuration:
```yaml
steps:
- plugins:
    - kubernetes-logs#v0.0.1:
        label_query: "release=production,component=web"
        namespace: default
```

Dynamic:
```yaml
steps:
- command: |
    buildkite-agent meta-data set "KUBERNETES_LOGS_LABEL_QUERY" "release=production,component=web"
  plugins:
    - kubernetes-logs#v0.0.1: {}
```
