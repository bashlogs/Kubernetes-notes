# Authorization

Once a request is authenticated, it needs to be authorized to be able to proceed through the Kubernetes system and perform its intended action.

There are three main authorization modes and two global Deny/Allow settings. The three main modes are:

* Node
* RBAC
* Webhook.

They can be configured as kube-apiserver startup options:

**--authorization-mode=Node,RBAC**

**--authorization-mode=Webhook**

The Node authorization is dedicated for kubelet to communicate to the kube-apiserver such that it does not need to be allowed via RBAC. All non-kubelet traffic would then be checked via RBAC.

The authorization modes implement policies to allow requests. Attributes of the requests are checked against the policies (e.g. user, group, namespace, verb).
