# NodePort

NodePort is a simple connection from a high-port routed to a ClusterIP using iptables, or ipvs in newer versions. The creation of a NodePort generates a ClusterIP by default. Traffic is routed from the NodePort to the ClusterIP. Only high ports can be used, as declared in the source code. The NodePort is accessible via calls to **\<NodeIP>:\<NodePort>**.

{% tabs %}
{% tab title="nodeport.yaml" %}
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
  type: NodePort
  selector:
    example: second      # App Name
  sessionAffinity: None
status:
  loadBalancer: {}
```

Command:

```
kubectl create -f nodeport.yaml
```
{% endtab %}
{% endtabs %}

Manually

{% code overflow="wrap" %}
```yaml
kubectl expose deployment mainapp --name=shopping --type=NodePort --port=80

kubectl expose deployment mainapp --name=shopping --type=NodePort --port=80 --target-port=8080
```
{% endcode %}
