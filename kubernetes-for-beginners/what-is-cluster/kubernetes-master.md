---
description: It's also called as master node
---

# Kubernetes Master

To manage multiple node we need a master node.

Master node controls and manages the worker nodes. The master node consists of several components that perform different functions, such as:

* **API Server**: The entry point for all REST commands to the cluster. It validates and forwards requests to other processes.
* **Scheduler**: The process that decides which worker node should host a new pod or component, based on the resources needed and available.
* **Controller Manager**: The process that runs various controllers that regulate the cluster state, such as node controller, replication controller, endpoints controller, etc.
* **etcd**: The distributed key-value store that stores the cluster configuration and state.

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>
