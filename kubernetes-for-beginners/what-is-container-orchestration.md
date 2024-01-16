# What is container orchestration ?

Container orchestration automates the provisioning, deployment, networking, scaling, availability, and lifecycle management of containers.

Today, [Kubernetes](https://www.ibm.com/topics/kubernetes) is the most popular container orchestration platform, and most leading public cloud providers - including Amazon Web Services (AWS), Google Cloud Platform, IBM Cloud and Microsoft Azure - offer managed Kubernetes services. Other container orchestration tools include Docker Swarm and Apache Mesos.

## How container orchestration works ?

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

While there are differences in methodologies and capabilities across tools, container orchestration is essentially a three-step process (or cycle, when part of an iterative agile or DevOps pipeline).

Most container orchestration tools support a declarative configuration model: A developer writes a configuration file (in YAML or JSON depending on the tool) that defines a desired configuration state, and the orchestration tool runs the file uses its own intelligence to achieve that state. The configuration file typically

* Defines which container images make up the application, and where they are located (in what registry)
* Provisions the containers with storage and other resources
* Defines and secures the network connections between containers
* Specifies versioning (for phased or canary rollouts)

The orchestration tool schedules deployment of the containers (and replicas of the containers, for resiliency) to a host, choosing the best host based on available CPU capacity, memory, or other requirements or constraints specified in the configuration file.&#x20;

Once the containers are deployed the orchestration tool manages the lifecycle of the containerized application based on the container definition file (very often a Dockerfile). This includes&#x20;

* Managing scalability (up and down), load balancing, and resource allocation among the containers
* Ensuring availability and performance by relocating the containers to another host in the event an outage or a shortage of system resources
* Collecting and storing log data and other telemetry used to monitor the health and performance of the application.



### Extra

#### Benefits of container orchestration

It's probably clear that the chief benefit of container orchestration is _automation -_ and not only only because it reduces greatly the effort and complexity of managing a large containerized application estate. By automating operations, orchestration supports an agile or DevOps approach that allows teams to develop and deploy in rapid, iterative cycles and release new features and capabilities faster.

In addition, an orchestration tool's intelligence can enhance or extend many of the inherent benefits of containerization. For example, automated host selection and resource allocation, based on declarative configuration, maximizes efficient use of computing resources; automated health monitoring and relocation of containers maximizes availability.
