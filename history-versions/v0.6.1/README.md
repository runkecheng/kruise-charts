# Kruise

## Install

Install with Helm 3:

If your Kubernetes version is lower than 1.15 and you'd like to install Kruise via Helm 3, you'll need Helm v3.1.0+ that has the flag --disable-openapi-validation.

```bash
# Kubernetes 1.14 and older versions
helm install kruise https://github.com/openkruise/kruise/releases/download/v0.6.2/kruise-chart.tgz --disable-openapi-validation
# Kubernetes 1.15 and newer versions
helm install kruise https://github.com/openkruise/kruise/releases/download/v0.6.2/kruise-chart.tgz
```

you will see follow:

```
NAME: kruise
LAST DEPLOYED: Mon Jan  6 14:47:48 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

## Uninstall

```bash
$ helm delete kruise
release "kruise" uninstalled
```

## Configuration

The following table lists the configurable parameters of the kruise chart and their default values.

| Parameter                                 | Description                                                  | Default                       |
| ----------------------------------------- | ------------------------------------------------------------ | ----------------------------- |
| `log.level`                               | Log level that kruise-manager printed                        | `4`                           |
| `revisionHistoryLimit`                    | Limit of revision history                                    | `3`                           |
| `manager.replicas`                        | Replicas of kruise-controller-manager deployment             | `2`                           |
| `manager.image.repository`                | Repository for kruise-manager image                          | `openkruise/kruise-manager`   |
| `manager.image.tag`                       | Tag for kruise-manager image                                 | `v0.6.2`                      |
| `manager.resources.limits.cpu`            | CPU resource limit of kruise-manager container               | `100m`                        |
| `manager.resources.limits.memory`         | Memory resource limit of kruise-manager container            | `256Mi`                       |
| `manager.resources.requests.cpu`          | CPU resource request of kruise-manager container             | `100m`                        |
| `manager.resources.requests.memory`       | Memory resource request of kruise-manager container          | `256Mi`                       |
| `manager.metrics.addr`                    | Addr of metrics served                                       | `localhost`                   |
| `manager.metrics.port`                    | Port of metrics served                                       | `8080`                        |
| `manager.webhook.port`                    | Port of webhook served                                       | `9443`                        |
| `manager.custom_resource_enable`          | Custom resources enabled by kruise-manager                   | `""(empty means all enabled)` |
| `spec.nodeAffinity`                       | Node affinity policy for kruise-manager pod                  | `{}`                          |
| `spec.nodeSelector`                       | Node labels for kruise-manager pod                           | `{}`                          |
| `spec.tolerations`                        | Tolerations for kruise-manager pod                           | `[]`                          |
| `webhookConfiguration.failurePolicy.pods` | The failurePolicy for pods in mutating webhook configuration | `Ignore`                      |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
# helm install kruise https://github.com/openkruise/kruise/releases/download/v0.6.2/kruise-chart.tgz --set manager.log.level=5,manager.custom_resource_enable="CloneSet\,SidecarSet"
```
