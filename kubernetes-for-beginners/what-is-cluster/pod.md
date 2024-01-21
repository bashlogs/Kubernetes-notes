# Pod

A Pod is the smallest unit in the Kubernetes ecosystem, akin to a container in the Docker world.

While multiple containers can coexist within a Pod, the recommended practice is often to have one primary container per Pod for efficiency. Additionally, multiple Pods can be deployed on a single worker node in a Kubernetes cluster.

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Extra&#x20;

#### Benefies of using pods

* Pods can run multiple containers that are tightly coupled and need to share resources, such as a web server and a sidecar container that updates the web content.
* Pods have a unique IP address and a set of ports within the cluster, and can communicate with other pods using the pod IP address.
* Pods can mount volumes for persistent or shared data among the containers in the pod.
* Pods can define health checks and readiness probes to monitor the status and availability of the containers.
* Pods can be managed by higher-level workload resources, such as deployments, statefulsets, or jobs, that provide features such as replication, rolling updates, or batch execution.

For more information: [https://www.tutorialspoint.com/kubernetes/kubernetes\_pod.htm](https://www.tutorialspoint.com/kubernetes/kubernetes\_pod.htm)





