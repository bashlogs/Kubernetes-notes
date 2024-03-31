# Table of contents

* [👋 Welcome to Kubernetes](README.md)
* [📚 Pre-Requirements](pre-requirements.md)

## Cluster Setup

* [Kubectl](cluster-setup/kubectl.md)
* [Minikube](cluster-setup/minikube.md)
* [K3s](cluster-setup/k3s.md)

## Architecture

* [What is Kubernetes](architecture/what-is-kubernetes.md)
* [The Borg Heritage](architecture/the-borg-heritage.md)
* [Kubernetes Arch.](architecture/kubernetes-arch..md)
* [Containers](architecture/containers.md)
* [Pods](architecture/pods.md)
* [Services](architecture/services.md)
* [Deployment](architecture/deployment.md)

## Build

* [Containerizion](build/containerizion.md)
* [Dockerfile](build/dockerfile.md)
* [Deployment](build/deployment.md)
* [Multi-Container Pod](build/multi-container-pod.md)

## Design

* [Resources Management](design/resources-management.md)
* [Label and Selector](design/label-and-selector.md)
* [Jobs and CronJobs](design/jobs-and-cronjobs.md)

## Deployments

* [Basic Commands](deployments/basic-commands.md)
* [Storage configs](deployments/storage-configs/README.md)
  * [Volumes](deployments/storage-configs/volumes.md)
  * [Volume Types](deployments/storage-configs/volume-types.md)
  * [PV and PVC](deployments/storage-configs/pv-and-pvc.md)
* [Config Maps / Secrets](deployments/config-maps-secrets.md)

## 🔐 Security

* [Accessing the API](security/accessing-the-api/README.md)
  * [Authentication](security/accessing-the-api/authentication.md)
  * [Authorization](security/accessing-the-api/authorization.md)
  * [Admission Controller](security/accessing-the-api/admission-controller.md)
* [Security Contest](security/security-contest/README.md)
  * [Pod Security Policies](security/security-contest/pod-security-policies.md)
  * [Pod Security Standard](security/security-contest/pod-security-standard.md)
* [Network Policies](security/network-policies/README.md)
  * [Example](security/network-policies/example.md)
* [Practical](security/practical/README.md)
  * [Security Context](security/practical/security-context.md)
  * [Create / Consume Secrets](security/practical/create-consume-secrets.md)
  * [Service Account](security/practical/service-account.md)
  * [Network Policies](security/practical/network-policies.md)
  * [Test Policy](security/practical/test-policy.md)
  * [Assignment](security/practical/assignment.md)

## Services

* [Service Types](services/service-types/README.md)
  * [Cluster IP](services/service-types/cluster-ip.md)
  * [NodePort](services/service-types/nodeport.md)
  * [LoadBalancer](services/service-types/loadbalancer.md)
* [Container Commands](services/container-commands.md)
* [Ingress Resources](services/ingress-resources.md)

## Others

* [NFS Server](others/nfs-server.md)
* [Shortcut](others/shortcut.md)
* [Podman](others/podman.md)
* [Overall Architecture](others/overall-architecture.md)
