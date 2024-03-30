# Security Contest

Pods and containers within pods can be given specific security constraints to limit what processes running in containers can do. For example, the UID of the process, the Linux capabilities, and the filesystem group can be limited.

Clusters installed using kubeadm allow pods any possible elevation in privilege by default. For example, a pod could control the nodes networking configuration, disable SELinux, override root, and more. These abilities are almost always limited by cluster administrators.

This security limitation is called a security context. It can be defined for the entire pod or per container, and is represented as additional sections in the resources manifests. A notable difference is that Linux capabilities are set at the container level.

{% code title="nginx.yaml" %}
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  securityContext:
    runAsNonRoot: true
  containers:
  - image: nginx
    name: nginx
```
{% endcode %}

