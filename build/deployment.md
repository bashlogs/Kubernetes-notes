# Deployment

## Creating a Deployment

Once you can push and pull images using the **podman**, **crictl** or **docker** commands, try to run a new deployment inside Kubernetes using the image. The string passed to the **--image** argument includes the repository to use, the name of the application, then the version.

```yaml
# Command:
kubectl create deployment simpleapp --image=username/simpleapp:1.0

# Check the deploy
​kubectl get pods

# To enter into a pod
kubectl exec -i​t <Pod-Name> -- /bin/bash
kubectl exec -i​t <Pod-Name> -c <Container-Name> -- sh
```



## Testing

With the decoupled and transient nature and great flexibility, there are many possible combinations of deployments. Each deployment would have its own method for testing. No matter which technology is implemented, the goal is the end user getting what is expected. Building a test suite for your newly deployed application will help speed up the development process and limit issues with the Kubernetes integration.

In addition to overall access, building tools which ensure the distributed application functions properly, especially in a transient environment, is a good idea.

While custom-built tools may be best at testing a deployment, there are some built-in **kubectl** arguments to begin the process. The first one is **describe** and the next would be **logs**.



```yaml
# Command
kubectl describe pod test1

# To check the output of container
kubectl logs test1

# A different pod may be configured to show lots of log output, such as the etcd pod
kubectl -n kube-system logs etcd-master
```
