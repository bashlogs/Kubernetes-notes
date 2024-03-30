# Ingress Resources

An ingress resource is an API object containing a list of rules matched against all incoming requests. Only HTTP rules are currently supported. In order for the controller to direct traffic to the backend, the HTTP request must match both the host and the path declared in the ingress.

## Ingress Controller

Handling a few services can be easily done. However, managing thousands or tens of thousands of services can create inefficiencies. The use of an ingress controller manages ingress rules to route traffic to existing services. Ingress can be used for fan out to services, name-based hosting, TLS, or load balancing. As security has become more of a concern, ingress controller pods are no longer given access to low-numbered ports. Instead, the assumption is a single high-numbered port, with an external load balancer in use to provide typical low-numbered ports.



<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
