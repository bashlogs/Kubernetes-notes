---
description: https://www.redhat.com/en/topics/containers/what-is-a-kubernetes-cluster
---

# What is Cluster ?

A Kubernetes cluster is a set of node machines for running containerized applications. If you’re running Kubernetes, you’re running a cluster.

### How does a cluster relate to a node, a pod, and other Kubernetes terms?

We’ve defined a cluster as a set of nodes. Let’s look at a few other Kubernetes terms that are helpful to understanding what a cluster does.

**Control plane:** The collection of processes that control Kubernetes nodes. This is where all task assignments originate.

**Pod:** A set of 1 or more containers deployed to a single node. A pod is the smallest and simplest Kubernetes object. [Click here](pod.md) to see pod architecture

**Node:** These machines perform the requested tasks assigned by the control plane. [Click here](node-worker-node.md) to see nodes architecture

**Service:** A way to expose an application running on a set of pods as a network service. This decouples work definitions from the pods.

**Volume:** A directory containing data, accessible to the containers in a pod. A Kubernetes volume has the same lifetime as the pod that encloses it. A volume outlives any containers that run within the pod, and data is preserved when a container restarts.

**Namespace:** A virtual cluster. Namespaces allow Kubernetes to manage multiple clusters (for multiple teams or projects) within the same physical cluster.

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>
