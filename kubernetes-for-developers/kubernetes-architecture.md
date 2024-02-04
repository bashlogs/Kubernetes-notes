# Kubernetes Architecture

Running a container on a laptop is relatively simple. Deploying and connecting containers across multiple hosts, scaling them, deploying applications without downtime, and service discovery among several aspects can be complex.

Kubernetes addresses those challenges from the start with a set of primitives and a powerful open and extensible API. The ability to add new objects and operators allows easy customization for various production needs. The ability to add multiple schedulers and multiple API servers adds to this customization.

Kubernetes can be an integral part of Continuous Integration/Continuous Delivery (CI/CD), as it offers many of the necessary components.

* **Continuous Integration**\
  A consistent way to build and test software. Deploying new packages with code written each day, or every hour, instead of quarterly. Tools like Helm and Jenkins are often part of this with Kubernetes.
* **Continuous Delivery**\
  An automated way to test and deploy software into various environments. Kubernetes handles the lifecycle of containers and connection of infrastructure resources to make rolling updates and rollbacks easy, among other deployment schemes.

There are several options and possible configurations when building a CI/CD pipeline. Tools such as Jenkins, Spinnaker, GitHub, GitLab and Helm, among others, may be part of your particular pipeline. To learn more about CI/CD take a look at the [_"DevOps and SRE Fundamentals: Implementing Continuous Delivery"_](https://training.linuxfoundation.org/training/devops-and-sre-fundamentals-implementing-continuous-delivery-lfs261/) (LFS261) course.

### Kuberneted Architecture

{% embed url="https://d36ai2hkxl16us.cloudfront.net/course-uploads/e0df7fbf-a057-42af-8a1f-590912be5460/x5fyaauz0qgq-Kubernetes_Architecture.png" %}



