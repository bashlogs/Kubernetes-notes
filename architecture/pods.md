# Pods

The whole point of Kubernetes is to orchestrate the life cycle of a container. We do not interact with particular containers. Instead, the smallest unit we can work with is a [Pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/).

A Pod is similar to a set of containers with shared namespaces and shared filesystem volumes.

Pods in a Kubernetes cluster are used in two main ways:

* **Pods that run a single container**. The "one-container-per-Pod" model is the most common Kubernetes use case; in this case, you can think of a Pod as a wrapper around a single container; Kubernetes manages Pods rather than managing the containers directly.
*   **Pods that run multiple containers that need to work together**. A Pod can encapsulate an application composed of [multiple co-located containers](https://kubernetes.io/docs/concepts/workloads/pods/#how-pods-manage-multiple-containers) that are tightly coupled and need to share resources. These co-located containers form a single cohesive unit.

    Grouping multiple co-located and co-managed containers in a single Pod is a relatively advanced use case. You should use this pattern only in specific instances in which your containers are tightly coupled.

### Run the pod using command

```
kubectl run newpod --image=nginx --generator=run-pod/v1
```

### Run the pod using a file

{% code title="simple-pod.yaml" %}
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```
{% endcode %}

```
kubectl apply -f simple-pod.yaml
```

### To view pods

```
kubectl get pods
kubectl get pods -o wide
```
