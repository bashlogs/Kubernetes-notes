---
description: Minikube automatically create a cluster for you.
---

# Cluster Setup

### Let's start the minikube

Command:&#x20;

```
minikube start --driver=<virtual machine name>
```

For Virtualbox:&#x20;

```
minikube start --driver=virtualbox --no-vtx-check

// Personal Configurations
minikube start --driver=virtualbox --memory 4000 --cpus 4 --no-vtx-check
```

For Docker

```
minikube start --driver=docker
```

For Hyper-v, hyperkit, parallels, vmware

```
minikube start --driver=hyperv
minikube start --driver=hyperkit
minikube start --driver=parallels
minikube start --driver=vmware
```

After Installation check the status:

```
minikube status
```

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/VirtualBox_JUDYAdqQTJ.png" alt=""><figcaption></figcaption></figure>

That's it, a single node cluster is successfully created in your machine.
