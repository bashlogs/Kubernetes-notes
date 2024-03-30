# Assignment

Focus on ensuing you have all the necessary files and processes understood first. Repeat the review until you are sure youhave the necessary YAML samples and can complete each step quickly, and ensure each object is running properly.

1\. Create a new deployment which uses thenginximage.

{% tabs %}
{% tab title="app1.yaml" %}
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app1
spec:
  selector:
    matchLabels:
      app: app1
  template:
    metadata:
      labels:
        app: app1
    spec:
      containers:
      - name: app1
        image: nginx
        ports:
        - containerPort: 80
```

Command

```
kubectl create -f app1.yaml
```
{% endtab %}
{% endtabs %}

2\. Create a newLoadBalancerservice to expose the newly created deployment. Test that it works.

```
kubectl expose deployment app1 --type=LoadBalancer --port=80
```

3\. Create a new NetworkPolicy called netblock which blocks all traffic to pods in this deployment only. Test that all traffic isblocked to deployment.



4\. Update thenetblockpolicy to allow traffic to the pod on port 80 only. Test that you can access the default nginx webpage.

5\. Find and use thesecurity-review1.yamlfile to create a pod.student@cp: ̃$ kubectl create -f security-review1.yaml

6\. View the status of the pod.

7\. Use the following commands to figure out why the pod has issues.student@cp: ̃

$ kubectl get pod securityreviewstudent@cp: ̃

$ kubectl describe pod securityreviewstudent@cp: ̃

$ kubectl logs securityreview

8\. After finding the errors, log into the container and find the proper id of the nginx user.

9\. Edit the yaml and re-create the pod such that the pod runs without error.

{% tabs %}
{% tab title="First Tab" %}
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: securityreview
  labels:
    app: security
spec:
  # securityContext:
  #   runAsUser: 2100
  containers:
  - name:  webguy
    image: nginx
    securityContext:
      runAsUser: 2000
      allowPrivilegeEscalation: false
```
{% endtab %}
{% endtabs %}

10\. Create a newserviceAccountcalled securityaccount.

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
 name: serviceaccount
```

11\. Create a ClusterRole named secrole which only allows create, delete, and list of pods in all apiGroups.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
 name: practice
rules:
- apiGroups:
  - ""
  resources:
  - pods
  verbs:
  - create
  - delete
  - list
```

12\. Bind the clusterRole to the serviceAccount.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
 name: practicedemo
subjects:
- kind: ServiceAccount
  name: serviceaccount
roleRef:
 kind: ClusterRole
 name: practice
 apiGroup: rbac.authorization.k8s.io
```

13\. Locate the token of the securityaccount. Create a file called/tmp/securitytoken. Put only the value oftoken:isequal to, a long string that may start with eyJh and be several lines long. Careful that only that string exists in the file.

```
kubectl get secret $(kubectl get sa securityaccount -o jsonpath='{.secrets[0].name}') -o go-template='{{.data.token | base64decode}}'
```

```
echo "<token-value>" > /tmp/securitytoken
```

14\. Remove any resources you have added during this review

```
kubectl delete rolebinding practicedemo
kubectl delete clusterrole practice
kubectl delete serviceaccount serviceaccount
```
