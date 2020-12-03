---
title: Kubernetes clusters using generic CSI drivers
linkTitle: Clusters with generic CSI Drivers
description: 
keywords:
weight: 5
disableprevnext: true
# scrollspy-container: false
---

PX-Backup supports backup and restore on Kubernetes clusters with generic CSI drivers if the driver meets certain prerequisites. 

{{<info>}}
**NOTE:** Portworx features native CSI driver support for cloud providers with their own native CSI driver support, such as AKS, EKS, and GKE. You do not need to follow these instructions to use PX-Backup on those clusters. Instead, see the page for your respective cloud provider.
{{</info>}}

## Prerequisites

Kubernetes prerequisites:

* Kubernetes clusters must be at least version 1.17 to use the Kubernetes CSI Snapshotting Beta feature.
* Kubernetes clusters must have the [snapshot-controller](https://github.com/kubernetes-csi/external-snapshotter/tree/master/deploy/kubernetes/snapshot-controller) version 3.0 or greater.

The generic CSI driver should implement the following:
  
* The CSI driver must include the [CSI snapshots and restores](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html) feature.
* The CSI driver must have the `snapshotter-sidecar` running at version 2.0 or greater.
* The CSI driver must have the `external-snapshotter` running at version 2.0 or greater.
* Ideally, the CSI driver should implement `ListSnapshots` for indicating that the snapshot is ready to use on the storage backend.
* For cross-cluster restores, the CSI drivers for both clusters will need to be connected to the same storage backend. In particular, the `snapshotHandle` used on the source cluster must be visible on the destination cluster via CSI `ListSnapshots`.

Portworx has tested and recommends the following CSI drivers for use with your Kubernetes clusters:

* Pure Storage PSO CSI Driver
* Openshift OCS RBD CSI Driver

## Add the cluster to PX-Backup

1. From the home page, select **Add Cluster**:

    ![Add cluster](/img/add-cluster.png)

2. On the **Add Kubernetes Cluster** page, enter the cluster details:

    * The name of the cluster
    * Retrieve the Kubeconfig from your cluster and paste it in the **Kubeconfig** text frame, or select the **Browse** button to upload it from a file.
    * Select the **Others** radio button from the **Kubernetes Service** radio group

    ![Enter the cluster details](/img/enter-other-kubernetes-distributions-cluster-details.png)

3. Select the **Submit** button

## CSI driver specific parameters
PX-Backup utilizes a `VolumeSnapshotClass` for performing generic CSI backups and restores. PX-Backup looks for a VolumeSnapshotClass with the naming scheme `"stork-csi-snapshot-class-${DRIVER_NAME}"` where `DRIVER_NAME` is the name of the CSI driver. You can find the CSI driver(s) for your cluster by running the following command:
```
kubectl get csidrivers
```

See your CSI driver documentation to determine which parameters are needed in the VolumeSnapshotClass. If the CSI driver you're using requires `VolumeSnapshotClass` parameters in order to function correctly, you will need to create or update this object. We will create this VolumeSnapshotClass with default values if it does not exist.
For fresh installs, create a VolumeSnapshotClass with the name `"stork-csi-snapshot-class-${DRIVER_NAME}"` based on your CSI driver documentation. Make sure all necessary parameters are added to this VolumeSnapshotClass.

If a CSI backup has already been attempted and failed, complete the following steps to edit the default VolumeSnapshotClass for your CSI driver:
1. Find the CSI driver(s) for your volumes
```
kubectl get csidrivers
```
2. Edit the VolumeSnapshotClass object for your CSI driver
```
CSI_DRIVER_NAME=<csi_driver_name>
kubectl edit volumesnapshotclass stork-csi-snapshot-class-${CSI_DRIVER_NAME}
```
3. Add the necessary parameters to this object based on the documentation for your CSI driver(s)
4. PX-Backup will now use these VolumeSnapshotClass parameters when performing backups and restores.

{{<info>}}
**NOTE:** PX-Backup always overrides the `VolumeSnapshotClass` with a deletion policy as retain to prevent data loss.
{{</info>}}
