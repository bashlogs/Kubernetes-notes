# Create / Consume Secrets

{% tabs %}
{% tab title="Secrets.yaml" %}
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: lfsecret
data:
  password: TEZUckAxbgo=
```

Commands:

```
kubectl create -f secrets.yaml
kubectl describe secret lfsecret
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="First Tab" %}
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secondapp
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - name: busy 
    image: busybox
    command:
      - sleep
      - "3600"
    securityContext:
      runAsUser: 2000
      allowPrivilegeEscalation: false 
      capabilities:
        add: ["NET_ADMIN", "SYS_TIME"]
    volumeMounts:
    - name: mysql
      mountPath: /mysqlpassword
  volumes:
  - name: mysql
    secret:
      secretName: lfsecret
```

Commands:

```
kubectl create -f .\second.yaml
kubectl exec -it secondapp -- /bin/sh
cat /mysqlpassword/password
```
{% endtab %}
{% endtabs %}
