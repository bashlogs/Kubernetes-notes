# LoadBalancer

Creating a **LoadBalancer** service generates a **NodePort**, which then creates a **ClusterIP**. It also sends an asynchronous call to an external load balancer, typically supplied by a cloud provider. The **External-IP** value will remain in a **\<Pending>** state until the load balancer returns. Should it not return, the **NodePort** created acts as it would otherwise.

{% tabs %}
{% tab title="loadbalancer.yaml" %}
```yaml
apiVersion: v1
kind: Service
metadata:
  name: secondapp
spec:
  ports:
  - port: 80
    protocol: TCP
    nodePort: 32000
  type: LoadBalancer
  selector:
    example: second
  sessionAffinity: None
status:
  loadBalancer: {}
```

Command:

```
kubectl create -f loadbalance.yaml
```
{% endtab %}
{% endtabs %}

Manually

{% code overflow="wrap" %}
```
kubectl expose deployment mainapp --name=shopping --type=LoadBalancer --port=80

kubectl expose deployment mainapp --name=shopping --type=LoadBalancer --port=80 --target-port=8080
```
{% endcode %}
