# Resources Management

In Kubernetes, you can manage CPU resources for your pods using resource requests and limits. This helps ensure fair resource allocation and prevents individual pods from monopolizing CPU resources, leading to a better overall performance and stability of your cluster. Here's how you can manage CPU resources in Kubernetes:

1. **Resource Requests**: Resource requests are the amount of CPU resources that Kubernetes guarantees to allocate to a pod when scheduling it onto a node. It's the minimum amount of CPU required by the pod to function properly.
2. **Resource Limits**: Resource limits define the maximum amount of CPU resources that a pod can consume. If a pod exceeds its CPU limit, Kubernetes throttles its CPU usage.

```yaml
spec:
      containers:
      - image: vish/stress
        imagePullPolicy: Always
        name: igottrouble
        resources:
          limits:
            cpu: "3"
            memory: "1Gi"
          requests:
            cpu: "2.5"
            memory: "500Mi"
        args:
        - -cpus
        - "2"
        - -mem-total
        - "1950Mi"
        - -mem-alloc-size
        - "100Mi"
        - -mem-alloc-sleep
        - "1s"
```

3. **Horizontal Pod Autoscaler (HPA)**: You can also utilize the Horizontal Pod Autoscaler to automatically scale the number of pods based on CPU utilization. The HPA adjusts the number of replicas of a Deployment, ReplicaSet, or StatefulSet based on observed CPU metrics.

```yaml
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: my-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-deployment
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
```
