# Services

The Service API, part of Kubernetes, is an abstraction to help you expose groups of Pods over a network. Each Service object defines a logical set of endpoints (usually these endpoints are Pods) along with a policy about how to make those pods accessible.

With every object and agent decoupled we need a flexible and scalable operator which connects resources together and will reconnect, should something die and a replacement is spawned. Each Service is a microservice handling a particular bit of traffic, such as a single NodePort or a LoadBalancer to distribute inbound requests among many Pods.

A Service also handles access policies for inbound requests, useful for resource control, as well as for security.

## Types of Services

### ClusterIP&#x20;

Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default that is used if you don't explicitly specify a type for a Service. You can expose the Service to the public internet using an Ingress or a Gateway.

### NodePort&#x20;

Exposes the Service on each Node's IP at a static port (the NodePort). To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: ClusterIP.

### LoadBalancer&#x20;

Exposes the Service externally using an external load balancer. Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider.

### ExternalName&#x20;

Maps the Service to the contents of the externalName field (for example, to the hostname api.foo.bar.example). The mapping configures your cluster's DNS server to return a CNAME record with that external hostname value. No proxying of any kind is set up.

## Defining a Service

{% code title="service.yaml" %}
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```
{% endcode %}

```
kubectl create -f service.yaml
```

## Directly expose services

```
kubectl expose deployment nginx-deployment --port=80 --type=NodePort
```

## Other Commands

<pre class="language-yaml"><code class="lang-yaml"># To get svc
kubectl get services

# To describe services
kubectl describe service &#x3C;service_name>
<strong>
</strong># To delete services
kubectl delete service &#x3C;service_name>
</code></pre>
