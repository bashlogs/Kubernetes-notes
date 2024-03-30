# Shortcut

Basic Pod

```
kubectl run basic2 --image=nginx --port=80 --rm=false --dry-run=client -o yaml > basic2.yaml
```

Service

{% code overflow="wrap" %}
```
kubectl create service clusterip webserver --tcp=80:80 --dry-run=client -o yaml > svc2.yaml
kubectl create service nodeport webserver --tcp=80:80 --dry-run=client -o yaml > svc2.yaml
```
{% endcode %}

Deployment

```
kubectl create deployment dep --image=nginx --dry-run=client -o yaml > deployment.yaml
```

Jobs

{% code overflow="wrap" %}
```
kubectl create job a1 --image=busybox --dry-run=client -o yaml -- /bin/sleep 3 > job.yaml
```
{% endcode %}

Cronjobs

{% code overflow="wrap" %}
```
k create cronjob cron --image=busybox --schedule="*/1 * * * *" --dry-run=client -o yaml -- /bin/sleep 3 > cronjob.yaml
```
{% endcode %}

configmap

{% code overflow="wrap" %}
```
kubectl create configmap fast-car --from-literal=car.make=Ford --from-literal=car.model=mustang --from-literal=car.trim=shelby --dry-run=client -o yaml > config.yaml
```
{% endcode %}



Security

```yaml
#Serviceaccount

k get serviceaccount secret-access-sa -o yaml > serviceaccount.yaml

#clusterroles

k create clusterrole secret-access-cr --verb=get,list --resource=secrets -o yaml > clusterrole.yaml

# rolebinding

apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: secret-rb
  namespace: default
subjects:
- kind: ServiceAccount
  name: secret-access-sa # "name" is case sensitive
roleRef:
  kind: ClusterRole #this must be Role or ClusterRole
  name: secret-access-cr # this must match the name of the Role or ClusterRole you wish to bind to
  apiGroup: rbac.authorization.k8s.io

#check the access

kubectl auth can-i get secrets --as=system:serviceaccount:default:secret-access-sa

# list auth
kubectl auth can-i --list --as=system:serviceaccount:default:secret-access-sa
```

k3s error

{% code overflow="wrap" %}
```
https://devops.stackexchange.com/questions/16043/error-error-loading-config-file-etc-rancher-k3s-k3s-yaml-open-etc-rancher
```
{% endcode %}

{% embed url="https://devops.stackexchange.com/questions/16043/error-error-loading-config-file-etc-rancher-k3s-k3s-yaml-open-etc-rancher" %}
