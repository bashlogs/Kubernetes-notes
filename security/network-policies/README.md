# Network Policies

While setting up network policies is done by cluster administrators, it is important to understand how they work and could prevent your microservices from communicating with each other or outside the cluster.

By default, all pods can reach each other all ingress and egress traffic is allowed. This has been a high-level networking requirement in Kubernetes. However, network isolation can be configured and traffic to pods can be blocked. In newer versions of Kubernetes, egress traffic can also be blocked. This is done by configuring a **NetworkPolicy**. As all traffic is allowed, you may want to implement a policy that drops all traffic, then, other policies which allow desired ingress and egress traffic.

The **spec** of the policy can narrow down the effect to a particular namespace, which can be handy. Further settings include a **podSelector**, or label, to narrow down which Pods are affected. Further ingress and egress settings declare traffic to and from IP addresses and ports.

