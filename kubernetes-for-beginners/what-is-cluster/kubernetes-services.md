# Kubernetes Services

A service is responsible for making our Pods discoverable inside the network or exposing them to the internet.

A Kubernetes service is a way to expose a network application that is running as one or more pods in your cluster.

A service provides a stable IP address and load balancing for the pods that match a selector.

There are 4 types of services:

* ClusterIP: This is the default type of service. It assigns a cluster-internal IP address to the service and exposes it within the cluster only.
* NodePort: This type of service allocates a port on each node and exposes the service on that port. It allows external access to the service via any node’s IP address and the allocated port.
* LoadBalancer: This type of service creates an external load balancer in the cloud provider and assigns a fixed, external IP address to the service. It allows external access to the service via the load balancer’s IP address and port.
* Ingress: This is not a service type, but a resource that acts as the entry point for your cluster. It allows you to define rules for routing HTTP traffic to different services based on the host name and path.
