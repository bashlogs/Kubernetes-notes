# 📚 Pre-Requirements

Before jumping into learning Kubernetes, you need to have a fair amount of knowledge of some of the underlying technologies and concepts.

1. **Distributed system:** Learn about distributed system basics & their use cases in modern IT infrastructure. [CAP theorem](https://devopscube.com/recommends/cap-therorem/) is good to have knowledge.
2. **Authentication & Authorization**: A very basic concept in IT. However, engineers starting their careers tend to get confused. So please get a good understanding of learning from analogies. You will quite often see these terms in Kubernetes.
3. **Key Value Store**: It is a type of NoSQL Database. Understand just enough basics and their use cases.
4. **API:** Kubernetes is an API-driven system. So you need to have an understanding of RESTFUL APIs. Also, try to understand gRPC API. It’s good to have knowledge.
5. **YAML**: YAML stands for _YAML Ain’t Markup Language_. It is a data serialization language that can be used for data storage and configuration files. It’s very easy to learn and from a Kubernetes standpoint, we will use it for configuration files. So understanding YAML syntax is very important.
6. **Container**: Container is the basic building block of Kubernetes. The primary work of Kubernetes is to orchestrate containers. You need to learn all the container basics and have hands-on experience working on container tools like Docker or Podman. I would also suggest reading about [Open container initiative](https://opencontainers.org/) and Container Runtime Interface (CRI)
7. [**Service Discovery**](https://devopscube.com/service-discovery-explained/): It is one of the key areas of Kubernetes. You need to have basic knowledge of client-side and server-side service discovery. To put it simply, in client-side service discovery, the **request goes to a service registry** to get the endpoints available for backend services. In server-side service discovery, the r**equest goes to a load balancer** and the load balancer uses the service registry to get the ending of backend services.
8. **Networking Basis**: Networking is a key part of Kubernetes. To understand Kubernetes networking, you need to have a fair knowledge of the following topics.
   1. CIDR Notation & Type of [IP Addresses](https://devopscube.com/ip-address-tutorial/)
   2. L2, L3, L4 & L7 Layers (OSI Layers)
   3. SSL/TLS: One way & Mutual TLS
   4. Proxy
   5. DNS
   6. IPVS/IPTables/NFtables
