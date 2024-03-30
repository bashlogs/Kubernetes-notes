# Containers

There are many competing organizations working with containers. As an orchestration tool, Kubernetes is being developed to work with many of them, with the overall community moving toward open standards and easy interoperability.&#x20;

The early and strong presence of Docker meant that historically, this was not the focus. As Docker evolved, spreading their vendor-lock characteristics through the container creation and deployment life cycle, new projects and features have become popular.&#x20;

As other container engines become mature, Kubernetes continues to become more open and independent.



## Container Runtime Interface

The goal of the Container Runtime Interface (CRI) is to allow easy integration of container runtimes with kubelet. By providing a protobuf method for API, specifications and libraries, new runtimes can easily be integrated without needing deep understanding of kubelet internals.



## Types of Containers

### 1. Containerd

The intent of the containerd project is not to build a user-facing tool; instead, it is focused on exposing highly-decoupled low-level primitives. Because of it modularity and low overhead, large cloud providers use this engine. User facing tools such as crictl, ctr, and nerdctl are being further developed.

* ​Defaults to runC to run containers according to the OCI Specifications
* Intended to be embedded into larger systems
* Minimal CLI, focused on debugging and development.

### 2. CRI-O

This project is currently in incubation as part of Kubernetes. It uses the Kubernetes Container Runtime Interface with OCI-compatible runtimes, thus the name [CRI-O](https://github.com/cri-o/cri-o). Currently, there is support for runC (default) and Clear Containers, but a stated goal of the project is to work with any OCI-compliant runtime.

### 3. Docker

Launched in 2013

Docker made containerizing, deploying, and consuming applications easy. As a result, it became the default option in production. With an open registry of images,&#x20;

[Docker Hub](https://hub.docker.com/), you can download and deploy vendor or individual-created images on multiple architectures with a single and easy to use toolset.&#x20;

This ease meant it was the sensible default choice for any developer as well. Issues with rapid updates and interaction with stakeholders lead to major vendors moving away from Docker soon after it became part of Mirantis.

### 4. rkt

The rkt runtime, pronounced rocket, provides a CLI for running containers. Announced by CoreOS in 2014, it is now part of the Cloud Native Computing Foundation family of projects.&#x20;

Learning from early Docker issues, it is focused on being more secure, open and interoperable. Many of its features have been met by Docker improvements.&#x20;

It is not quite an easy drop-in replacement for Docker, but progress has been made. rkt uses the appc specification, and can run Docker, appc and OCI images. It deploys immutable pods.





