---
description: How to modify the container runtime
---

# Container Runtime

To change to container runtime of minikube from docker to containerd or ORI-D

First stop the minikube

```
minikube stop
```

Delete the minikube

```
minikube delete
```

Create the new virtual machine with your preffered container runtime

```
// For cri-o container 
minikube start --drive=virtualbox --container-runtime=cri-o

// For containerd
minikube start --drive=virtualbox --container-runtime=containerd
```

