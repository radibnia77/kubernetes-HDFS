---
layout: global
title: HDFS on Kubernetes
---
# HDFS on Kubernetes
Repository holding helm charts for running Hadoop Distributed File System (HDFS)
on Kubernetes.

See [charts/README.md](charts/README.md) for how to run the charts.

See [tests/README.md](tests/README.md) for how to run integration tests for
HDFS on Kubernetes.


Most of the developers face this issue because most of the tutorials have old YAML files and the support for extensions/v1beta1 was removed in v1.16, hence while applying the YAML configuration using the kubectl command we get this issue.

HDFS can be easily deployed using a ready-made Helm chart provided here. The Helm chart provides HA as well as a simple HDFS setup. As of writing this article, I used Kubernetes version 1.20 and as such, I had to make certain modifications to the charts.
Update the apiVersion for StatefulSets and DaemonSets as they are now in apps/v1
Make sure you have dynamic provisioning enabled for your cluster. If not, then you need to create PersistantVolumes for the StatefulSets (that includes Journal, Zookeeper and Namenodes).
In requirements.yaml file (inside hdfs-k8s directory), change the Zookeeper repository to https://charts.helm.sh/incubator and version to 2.1.6
There was no option to update the storage class of Zookeeper inside values.yaml, so you can update that section as below.

helm dep update charts/hdfs-k8s/
helm dependency build charts/hdfs-k8s

//make sure there is noting with my-hdfs in kube
helm install my-hdfs charts/hdfs-k8s

HDFS on K8s stores the file data on the local disks of the K8s cluster nodes
using K8s HostPath volumes. You may want to change the default locations. Set
global.dataNodeHostPath to override the default value. Note the option
takes a list in case you want to use multiple disks.

```
  $ helm install my-hdfs charts/hdfs-k8s  \
      --set "global.dataNodeHostPath={/mnt/sda1/data0,/mnt/sda1/hdfs-data1}"
```
