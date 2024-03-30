# Pod Security Policies

To automate the enforcement of security contexts, you can define [PodSecurityPolicies](https://kubernetes.io/docs/concepts/policy/pod-security-policy/) (PSP). A PSP is defined via a standard Kubernetes manifest following the PSP API schema. An example is presented below. Be aware that due to usability issues and confusion, PSPs have been deprecated. The replacement has not fully been decided. You can read more about it in the ["PodSecurityPolicy Deprecation: Past, Present, and Future"](https://kubernetes.io/blog/2021/04/06/podsecuritypolicy-deprecation-past-present-and-future/) blog post.

These policies are cluster-level rules that govern what a pod can do, what they can access, what user they run as, etc.

For instance, if you do not want any of the containers in your cluster to run as the root user, you can define a PSP to that effect. You can also prevent containers from being privileged or use the host network namespace, or the host PID namespace.

{% code title="" %}
```yaml
apiVersion: policy/v1beta1
kind: PodSecurityPolicy
metadata:
  name: restricted
spec:
  seLinux:
    rule: RunAsAny
  supplementalGroups:
    rule: RunAsAny
  runAsUser:
    rule: MustRunAsNonRoot
  fsGroup:
    rule: RunAsAny
```
{% endcode %}

Examples

{% embed url="https://github.com/kubernetes/examples/blob/master/staging/podsecuritypolicy/rbac/README.md" %}
