# Node / Worker Node

Nodes are actually machines/server and you can include such multiple server in a cluster.

This service runs on each worker node and its job is to manage the container. It makes sure containers are running and healthy and it connects back to the control plane. Kubelet talks to the API server and it is responsible for managing resources on the node it's running on.

* **Kubelet**: The agent that runs on each node and communicates with the API server. It manages the pods and containers on the node, and reports the node status to the master.
* **Kube-proxy**: The network proxy that runs on each node and maintains the network rules and connections.
* **Container runtime**: The software that runs and manages the containers, such as Docker, containerd, CRI-O, etc.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Worker Node</p></figcaption></figure>

### Extra

For more information: [https://www.tutorialspoint.com/kubernetes/kubernetes\_node.htm](https://www.tutorialspoint.com/kubernetes/kubernetes\_node.htm)
