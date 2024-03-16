---
description: Practical Stuff
---

# Practical with minikube

## Requirements

### For Cluster Management

Deploying big clusters on the cloud could be expensive.&#x20;

These are the paid services you can use :&#x20;

1. [GKE](https://devopscube.com/setup-kubernetes-cluster-google-cloud/) (Google Cloud – $300 free credits)
2. [EKS](https://devopscube.com/create-aws-eks-cluster-eksctl/) (AWS – $300 free POC credits)
3. [DO Kubernetes](https://devopscube.com/recommends/digital-ocean-sidebar/) (Digital Ocean – $200 free credits)
4. [Linode Kubernetes Engine](https://devopscube.com/recommends/linode-credits/) (Linode Cloud – $100 Free credits)
5. [Vultr Kubernetes Engine](https://devopscube.com/recommends/vultr-credits/) (Vultr Cloud – $250 Free Credits)

But in this practical we are going to make use of the free tool and create our own cluster locally.&#x20;

### [MiniKube](https://minikube.sigs.k8s.io/docs/)

Minikube is a free tool which allow you to create cluster with single node locally in your machine.&#x20;

We are going to use minikube throughout this practical.

There are some requirement for minikube also. We need a virtual machine for remote access to minikube. you can consider the following virtual machine platforms

* Virtual box: Suggestion for mac users
* VMware
* Docker: You can only run minikube as a container in docker
* Hyper-V: Suggestion for windows users
* Parallels

**Note that: Minikube allowes only one node per cluster**

To learn more about minikube: [https://minikube.sigs.k8s.io/docs/](https://minikube.sigs.k8s.io/docs/)

#### Let's start with the installation...
