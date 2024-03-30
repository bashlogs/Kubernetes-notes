# Admission Controller

The last step in completing an API request is one or more admission controls.

Admission controllers are pieces of software that can access the content of the objects being created by the requests. They can modify the content or validate it, and potentially deny the request.

Admission controllers are needed for certain features to work properly. Controllers have been added as Kubernetes matured. Starting with the 1.13.1 release of the **kube-apiserver**, the admission controllers are now compiled into the binary, instead of a list passed during execution. To enable or disable, you can pass the following options, changing out the plugins you want to enable or disable:

**--enable-admission-plugins=NamespaceLifecycle,LimitRanger**\
**--disable-admission-plugins=PodNodeSelector**

Controllers becoming more common are **MutatingAdmissionWebhook** and **ValidatingAdmissionWebhook**, which will allow the dynamic modification of the API request, providing greater flexibility. These calls reference an exterior service, such as OPA, and wait for a return API call. Each admission controller functionality is explained in the documentation. For example, the **ResourceQuota** controller will ensure that the object created does not violate any of the existing quotas. More information can be found on the [Dynamic Admission Control](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/) page in the Kubernetes documentation.
