# Build

## Container Options

A container runtime is the component which runs the containerized application upon request. Docker Engine was common, though containerd and CRI-O and others are gaining community support. We will be using containerd in the labs.

The Open Container Initiative (OCI) was formed to help with flexibility and the use of any desired engine. Docker donated their libcontainer project to form a new codebase called runC to support these goals. More information about [runC](https://github.com/opencontainers/runc) can be found on GitHub.

Where Docker was once the only real choice for developers, the trend toward open specifications and flexibility indicates that building with vendor-neutral features is a wise choice. Now that Docker is owned by Mirantis, many vendors have gone to other tools, such as [open source options found on GitHub](https://github.com/containers).



## Container Runtime Interface (CRI)

The goal of the Container Runtime Interface (CRI) is to allow easy integration of container runtimes with kubelet. By providing a protobuf method for API, specifications and libraries, new runtimes can easily be integrated without needing deep understanding of kubelet internals.

The project is in early stage, with lots of development in action. Now that Docker-CRI integration is done, new runtimes should be easily added and swapped out. At the moment, CRI-O, rktlet and frakti are listed as work-in-progress.



## containerd

The intent of the containerd project is not to build a user-facing tool; instead, it is focused on exposing highly-decoupled low-level primitives. Because of it modularity and low overhead, large cloud providers use this engine. User facing tools such as crictl, ctr, and nerdctl are being further developed.

* ​Defaults to runC to run containers according to the OCI Specifications
* Intended to be embedded into larger systems
* Minimal CLI, focused on debugging and development.

With a focus on supporting the low-level, or backend, plumbing of containers, this project is better suited to integration and operation teams building specialized products, instead of typical build, ship, and run application.



## CRI-O

This project is currently in incubation as part of Kubernetes. It uses the Kubernetes Container Runtime Interface with OCI-compatible runtimes, thus the name [CRI-O](https://github.com/cri-o/cri-o). Currently, there is support for runC (default) and Clear Containers, but a stated goal of the project is to work with any OCI-compliant runtime.

While newer than Docker or rkt, this project has gained major vendor support due to its flexibility and compatibility.



