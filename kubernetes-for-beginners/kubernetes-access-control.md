---
description: >-
  Authentication, Authorization, and Admission Control are three important
  aspects of Kubernetes access control.
---

# Kubernetes Access Control

### Authentication

**Authentication** is the process of verifying the identity of a user or a service account who wants to access the Kubernetes API server. Kubernetes supports various methods of authentication, such as certificates, tokens, basic auth, etc. [Authentication does not determine what actions the user can perform, only who they are.](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)

### Authorization

**Authorization** is the process of determining whether a user or a service account is allowed to perform a specific action on a resource in the cluster. Kubernetes supports various methods of authorization, such as RBAC, ABAC, Node, Webhook, etc. [Authorization is applied after authentication, and before admission control.](https://blog.kubesimplify.com/kubernetes-access-control-with-authentication-authorization-admission-control)

### Admission Control

**Admission Control** is the process of modifying or validating requests to the Kubernetes API server before they are persisted or executed. Admission controllers are plugins that implement specific policies or features, such as resource limits, pod security, default values, etc. [Admission control is applied after authorization, and only for mutating requests (not read-only requests).](https://wyssmann.com/blog/2021/06/authentication-and-authorization-in-kubernetes/)
