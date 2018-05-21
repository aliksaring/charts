# Dell EMC VxFlex Open Storage CSI Driver
> **NOTE:** Dell EMC VxFlex Open Storage was previously known as _ScaleIO_.

## TL;DR;

Add the repo (if you haven't already):
```bash
$ helm repo add vxflex https://vxflex-os.github.io/charts
```

Install the driver:
```bash
$ helm install --name vxflex-csi --namespace vxflexos --values=myvals.yaml
```

## Introduction

This chart bootstraps the VxFlexOS CSI driver on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.9+ with Beta APIs enabled
- VxFlex OS storage data client (SDC) deployed and configured on each Kubernetes worker node
- VxFlex OS REST API gateway (with approved VxFlex certificate)
- VxFlex OS configured storage pool

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release --values=myvals.yaml vxflex-csi
```
> **Tip**: List all releases using `helm list`

There are a number of required values that must be set either via the command-line or a [`values.yaml`](values.yaml) file. Those values are listed in the configuration section below.

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release [--purge]
```

The command removes all the Kubernetes components associated with the chart and deletes the release. The purge option also removes the provisioned release name, so that the name itself can also be reused.

## Configuration

The following table lists the primary configurable parameters of the VxFlexOS driver chart and their default values. More detailed information can be found in the [`values.yaml`](values.yaml) file in this repository.

| Parameter | Description | Required | Default |
| --------- | ----------- | -------- |-------- |
| systemName | Name of the VxFlex system   | true | - |
| username | Admin user of the VxFlex system   | true | - |
| password | Admin password of the VxFlex system   | true | - |
| restGateway | REST API gateway HTTPS endpoint VxFlex system | true | - |
| storagePool | VxFlex Storage Pool to use with in the Kubernetes storage class | true | - |
| volumeNamePrefix | String to prepend to any volumes created by the driver | false | csivol |
| controllerCount | Number of driver controllers to create | false | 1 |
| storageClass.name | Name of the storage class to be defined | false | vxflex |
| storageClass.isDefault | Whether or not to make this storage class the default | false | true |
| storageClass.reclaimPolicy | What should happen when a volume is removed | false | Delete |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name vxflex-csi --namespace vxflex \
  --set systemName=vxflex,username=admin,password=vxflex123,restGateway=https://123.0.0.1,storagePool=sp \
    vxflex-csi
```
Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml vxflex-csi
```

```yaml
# values.yaml

systemName: vxflex
username: admin
password: vxflex123
restGateway: 123.0.0.1
storagePool: sp
```

> **Tip**: You can add required parameters and then use the default [`values.yaml`](values.yaml)
