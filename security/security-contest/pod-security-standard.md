# Pod Security Standard

There are three policies to limit what a pod is allowed to do. These policies are cumulative. The namespace is given the appropriate label for each policy. New pods will then be restricted. Existing pods would not be changed by an edit to the namespace. Expect the particular fields and allowed values to change as the feature matures.

***

**Privileged** - No restrictions from this policy. Details can be found in the [Kubernetes documentation](https://kubernetes.io/docs/concepts/security/pod-security-standards/#privileged).

```yaml
apiVersion: v1
kind: Namespace
metadata: 
  name: no-restrictions-namespace
  labels:
    pod-security.kubernetes.io/enforce: privileged
    pod-security.kubernetes.io/enforce-version: latest
```

***

**Baseline** - Minimal restrictions. Does not allow known privilege escalations. Details can be found in the [Kubernetes documentation](https://kubernetes.io/docs/concepts/security/pod-security-standards/#baseline).

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: baseline-namespace
  labels:
    pod-security.kubernetes.io/enforce: baseline
    pod-security.kubernetes.io/enforce-version: latest
    pod-security.kubernetes.io/warn: baseline
    pod-security.kubernetes.io/warn-version: latest
```

***

**Restricted** - Most restricted policy. Follows current pod hardening best practices. Details can be found in the [Kubernetes documentation](https://kubernetes.io/docs/concepts/security/pod-security-standards/#restricted).

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-restricted-namespace
  labels:
    pod-security.kubernetes.io/enforce: restricted
    pod-security.kubernetes.io/enforce-version: latest
    pod-security.kubernetes.io/warn: restricted
    pod-security.kubernetes.io/warn-version: latest
```
