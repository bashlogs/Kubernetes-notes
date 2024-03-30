# Service Account

#### Create a service account

{% code title="serviceaccount.yaml" %}
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
 name: secret-access-sa
```
{% endcode %}

```
kubectl create -f serviceaccount.yaml
kubectl get serviceaccounts
```

#### Get the clusterroles

```
kubectl get clusterroles
kubectl get clusterroles admin -o yaml
kubectl get clusterroles cluster-admin -o yaml
```



Create a clusterrole

{% tabs %}
{% tab title="clusterroles.yaml" %}
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
 name: secret-access-cr
rules:
- apiGroups:
  - ""
  resources:
  - secrets
  verbs:
  - get
  - list
```

Command:

```
kubectl create -f clusterroles.yaml
kubectl get clusterroles secret-access-cr -o yaml
```
{% endtab %}
{% endtabs %}

Now bind the roles to the account `secret-access-sa`

{% tabs %}
{% tab title="rolebinding.yaml" %}
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
 name: secret-rb
subjects:
- kind: ServiceAccount
  name: secret-access-sa
roleRef:
 kind: ClusterRole
 name: secret-access-cr
 apiGroup: rbac.authorization.k8s.io
```

Commands:

```
kubectl create -f rolebinding.yaml
kubectl get rolebinding
kubectl get rolebinding secret-rb -o yaml
```
{% endtab %}
{% endtabs %}



Check the serviceaccount of one of your pod

```
kubectl get pod secondapp -o yaml | grep serviceAccount

# The output will have default entries
```



{% code title="second.yaml" %}
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secondapp
spec:
  serviceAccountName: secret-access-sa    # Changes are done here
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
{% endcode %}

Now create the pod and check serviceaccounts

```
kubectl create -f second.yaml
kubectl get pod secondapp -o yaml | grep serviceAccount
```
