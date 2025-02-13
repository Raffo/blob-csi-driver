#### Breaking change
From `v0.7.0`, driver name changed from `blobfuse.csi.azure.com` to `blob.csi.azure.com`, volume created by `v0.6.0`(or prior version) could not be mounted by `v0.7.0` driver. If you have volumes created by `v0.6.0` version, DO NOT upgrade to `v0.7.0` or higher version.

# Install CSI driver with Helm 3

## Prerequisites
 - [install Helm](https://helm.sh/docs/intro/quickstart/#install-helm)

## install latest version
```console
helm repo add blob-csi-driver https://raw.githubusercontent.com/kubernetes-sigs/blob-csi-driver/master/charts
helm install blob-csi-driver blob-csi-driver/blob-csi-driver --namespace kube-system
```

## install on Azure Stack
```console
helm install blob-csi-driver blob-csi-driver/blob-csi-driver --namespace kube-system --set cloud=AzureStackCloud
```

### install a specific version
```console
helm repo add blob-csi-driver https://raw.githubusercontent.com/kubernetes-sigs/blob-csi-driver/master/charts
helm install blob-csi-driver blob-csi-driver/blob-csi-driver --namespace kube-system --version v1.1.0
```

### search for all available chart versions
```console
helm search repo -l blob-csi-driver
```

## uninstall CSI driver
```console
helm uninstall blob-csi-driver -n kube-system
```

## latest chart configuration

The following table lists the configurable parameters of the latest Azure Blob Storage CSI driver chart and default values.

| Parameter                                             | Description                                           | Default                                                        |
| ----------------------------------------------------- | ----------------------------------------------------- | -------------------------------------------------------------- |
| `image.blob.repository`                               | blob-csi-driver docker image                          | mcr.microsoft.com/k8s/csi/blob-csi                             |
| `image.blob.tag`                                      | blob-csi-driver docker image tag                      | latest                                                         |
| `image.blob.pullPolicy`                               | blob-csi-driver image pull policy                     | IfNotPresent                                                   |
| `image.csiProvisioner.repository`                     | csi-provisioner docker image                          | mcr.microsoft.com/oss/kubernetes-csi/csi-provisioner           |
| `image.csiProvisioner.tag`                            | csi-provisioner docker image tag                      | v2.1.0                                                         |
| `image.csiProvisioner.pullPolicy`                     | csi-provisioner image pull policy                     | IfNotPresent                                                   |
| `image.livenessProbe.repository`                      | liveness-probe docker image                           | mcr.microsoft.com/oss/kubernetes-csi/livenessprobe             |
| `image.livenessProbe.tag`                             | liveness-probe docker image tag                       | v2.2.0                                                         |
| `image.livenessProbe.pullPolicy`                      | liveness-probe image pull policy                      | IfNotPresent                                                   |
| `image.nodeDriverRegistrar.repository`                | csi-node-driver-registrar docker image                | mcr.microsoft.com/oss/kubernetes-csi/csi-node-driver-registrar |
| `image.nodeDriverRegistrar.tag`                       | csi-node-driver-registrar docker image tag            | v2.0.1                                                         |
| `image.nodeDriverRegistrar.pullPolicy`                | csi-node-driver-registrar image pull policy           | IfNotPresent                                                   |
| `image.csiResizer.repository`                         | csi-resizer docker image                              | mcr.microsoft.com/oss/kubernetes-csi/csi-resizer               |
| `image.csiResizer.tag`                                | csi-resizer docker image tag                          | v1.1.0                                                         |
| `image.csiResizer.pullPolicy`                         | csi-resizer image pull policy                         | IfNotPresent                                                   |
| `imagePullSecrets`                                    | Specify docker-registry secret names as an array      | [] (does not add image pull secrets to deployed pods)          |
| `serviceAccount.create`                               | whether create service account of csi-blob-controller | true                                                           |
| `rbac.create`                                         | whether create rbac of csi-blob-controller            | true                                                           |
| `controller.replicas`                                 | the replicas of csi-blob-controller                   | 2                                                              |
| `controller.metricsPort`                              | metrics port of csi-blob-controller                   | 29634                                                          |
| `controller.runOnMaster`                              | run controller on master node                         | false                                                          |
| `controller.logLevel`                                 | controller driver log level                           | `5`                                                            |
| `controller.resources.csiProvisioner.limits.cpu`      | csi-provisioner cpu limits                            | 100m                                                           |
| `controller.resources.csiProvisioner.limits.memory`   | csi-provisioner memory limits                         | 100Mi                                                          |
| `controller.resources.csiProvisioner.requests.cpu`    | csi-provisioner cpu requests limits                   | 10m                                                            |
| `controller.resources.csiProvisioner.requests.memory` | csi-provisioner memory requests limits                | 20Mi                                                           |
| `controller.resources.livenessProbe.limits.cpu`       | liveness-probe cpu limits                             | 100m                                                           |
| `controller.resources.livenessProbe.limits.memory`    | liveness-probe memory limits                          | 300Mi                                                          |
| `controller.resources.livenessProbe.requests.cpu`     | liveness-probe cpu requests limits                    | 10m                                                            |
| `controller.resources.livenessProbe.requests.memory`  | liveness-probe memory requests limits                 | 20Mi                                                           |
| `controller.resources.blob.limits.cpu`                | blob-csi-driver cpu limits                            | 200m                                                           |
| `controller.resources.blob.limits.memory`             | blob-csi-driver memory limits                         | 200Mi                                                          |
| `controller.resources.blob.requests.cpu`              | blob-csi-driver cpu requests limits                   | 10m                                                            |
| `controller.resources.blob.requests.memory`           | blob-csi-driver memory requests limits                | 20Mi                                                           |
| `controller.resources.csiResizer.limits.cpu`          | csi-resizer cpu limits                                | 100m                                                           |
| `controller.resources.csiResizer.limits.memory`       | csi-resizer memory limits                             | 300Mi                                                          |
| `controller.resources.csiResizer.requests.cpu`        | csi-resizer cpu requests limits                       | 10m                                                            |
| `controller.resources.csiResizer.requests.memory`     | csi-resizer memory requests limits                    | 20Mi                                                           |
| `controller.affinity`                                 | controller pod affinity                               | {}                                                             |
| `controller.nodeSelector`                             | controller pod node selector                          | {}                                                             |
| `controller.tolerations`                              | controller pod tolerations                            | []                                                             |
| `node.metricsPort`                                    | metrics port of csi-blob-node                         | 29635                                                          |
| `node.logLevel`                                       | node driver log level                                 | `5`                                                            |
| `node.enableBlobfuseProxy`                            | node enable blobfuse-proxy                            | false                                                          |
| `node.resources.livenessProbe.limits.cpu`             | liveness-probe cpu limits                             | 100m                                                           |
| `node.resources.livenessProbe.limits.memory`          | liveness-probe memory limits                          | 100Mi                                                          |
| `node.resources.livenessProbe.requests.cpu`           | liveness-probe cpu requests limits                    | 10m                                                            |
| `node.resources.livenessProbe.requests.memory`        | liveness-probe memory requests limits                 | 20Mi                                                           |
| `node.resources.nodeDriverRegistrar.limits.cpu`       | csi-node-driver-registrar cpu limits                  | 100m                                                           |
| `node.resources.nodeDriverRegistrar.limits.memory`    | csi-node-driver-registrar memory limits               | 100Mi                                                          |
| `node.resources.nodeDriverRegistrar.requests.cpu`     | csi-node-driver-registrar cpu requests limits         | 10m                                                            |
| `node.resources.nodeDriverRegistrar.requests.memory`  | csi-node-driver-registrar memory requests limits      | 20Mi                                                           |
| `node.resources.blob.limits.cpu`                      | blob-csi-driver cpu limits                            | `2`                                                            |
| `node.resources.blob.limits.memory`                   | blob-csi-driver memory limits                         | 2100Mi                                                         |
| `node.resources.blob.requests.cpu`                    | blob-csi-driver cpu requests limits                   | 10m                                                            |
| `node.resources.blob.requests.memory`                 | blob-csi-driver memory requests limits                | 20Mi                                                           |
| `node.affinity`                                       | node pod affinity                                     | {}                                                             |
| `node.nodeSelector`                                   | node pod node selector                                | {}                                                             |
| `node.tolerations`                                    | node pod tolerations                                  | []                                                             |
| `kubelet.linuxPath`                                   | configure the kubelet path for Linux node             | `/var/lib/kubelet`                                             |
| `cloud`                                               | the cloud environment the driver is running on        | AzurePublicCloud                                               |
| `podAnnotations`                                      | collection of annotations to add to all the pods      | {}                                                             |
| `podLabels`                                           | collection of labels to add to all the pods           | {}                                                             |
| `priorityClassName`                                   | priority class name to be added to pods               | system-cluster-critical                                        |
| `securityContext`                                     | security context to be added to pods                  | {}                                                             |
| `node.livenessProbe.healthPort `                      | the health check port for liveness probe              | `29633` |

## troubleshooting
 - Add `--wait -v=5 --debug` in `helm install` command to get detailed error
 - Use `kubectl describe` to acquire more info
