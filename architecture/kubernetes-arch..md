# Kubernetes Arch.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

In its simplest form, Kubernetes is made of one or more central managers (aka masters) and worker nodes. The manager runs an API server, a scheduler, various operators and a datastore to keep the state of the cluster, container settings, and the networking configuration.

Kubernetes exposes an API via the API server. you can communicate with the API using a local client called kubectl or you can write your own client. The kube-scheduler sees the API requests for running a new container and finds a suitable node to run that container.&#x20;

Each node in the cluster runs two components: kubelet and kube-proxy. The kubelet systemd service receives spec information for container configuration, downloads and manages any necessary resources and works with the container engine on the local node to ensure the container runs or is restarted upon failure. The kube-proxy pod creates and manages local firewall rules and networking configuration to expose containers on the network.



## Control Plane Nodes

The Kubernetes master runs various server and manager processes for the cluster. Among the components of the master node are the kube-apiserver, the kube-scheduler, and the etcd database. As the software has matured, new components have been created to handle dedicated needs, such as the cloud-controller-manager; it handles tasks once handled by the kube-controller-manager to interact with other tools, such as Rancher or DigitalOcean for third-party cluster management and reporting.

### 1. Kube-apiserver

All calls, both internal and external traffic, are handled via this agent. All actions are accepted and validated by this agent, and it is the only agent which connects to the etcd database. As a result, it acts as a master process for the entire cluster, and acts as a frontend of the cluster's shared state. Each API call goes through three steps: authentication, authorization, and several admission controllers.

### 2. Kube Scheduler

The kube-scheduler uses an algorithm to determine which node will host a Pod of containers. The scheduler will try to view available resources (such as available CPU) to bind, and then assign the Pod based on availability and success. The scheduler uses pod-count by default, but complex configuration is often done if cluster-wide metrics are collected.

### 3. etcd Database

The state of the cluster, networking, and other persistent information is kept in an etcd database, or, more accurately, a _b+tree_ key-value store. Rather than finding and changing an entry, values are always appended to the end. Previous copies of the data are then marked for future removal by a compaction process. It works with curl and other HTTP libraries, and provides reliable watch queries.

### 4. Kube Controller Manager

The kube-controller-manager is a core control loop daemon which interacts with the kube-apiserver to determine the state of the cluster. If the state does not match, the manager will contact the necessary controller to match the desired state. There are several controllers in use, such as endpoints, namespace, and replication. The full list has expanded as Kubernetes has matured.



## Worker Node

All worker nodes run the kubelet and kube-proxy, as well as the container engine, such as containerd or cri-o. Other management daemons are deployed to watch these agents or provide services not yet included with Kubernetes.

### Kubelet

The kubelet interacts with the underlying Docker Engine also installed on all the nodes, and makes sure that the containers that need to run are actually running. The kubelet agent is the heavy lifter for changes and configuration on worker nodes. It accepts the API calls for Pod specifications (a PodSpec is a JSON or YAML file that describes a Pod). It will work to configure the local node until the specification has been met.

### Kube-proxy

The kube-proxy is in charge of managing the network connectivity to the containers. It does so through the use of iptables entries. It also has the userspace mode, in which it monitors Services and Endpoints using a random high-number port to proxy traffic. Use of ipvs can be enabled, with the expectation it will become the default, replacing iptables.
