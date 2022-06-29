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

As per the official documentation of Kubernetes (Release notes - 1.16.0)

The following APIs are no longer served by default:

All resources under apps/v1beta1 and apps/v1beta2 - use apps/v1 instead

daemonsets, deployments, replicasets resources under extensions/v1beta1 - use apps/v1 instead

networkpolicies resources under extensions/v1beta1 - use networking.k8s.io/v1 instead

podsecuritypolicies resources under extensions/v1beta1 - use policy/v1beta1 instead

make sure use to build after a change.
helm dependency build charts/hdfs-k8s
