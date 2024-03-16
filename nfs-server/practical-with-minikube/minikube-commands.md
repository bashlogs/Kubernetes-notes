# Minikube commands

### Basic minikube commands

Since we have successfully setup minikube we can check ip address.

```
minikube ip
```

This ip address to help us login in our minikube and it can also used to see our website once we deploy it.

#### For SSH login in your minikubes

```
ssh docker@192.168.59.101

// Minikube user cridential
username: docker
password: tcuser
```

Their is also another ways of direct login

```
ssh -i ~/.minikube/machines/minikube/id_rsa docker@192.168.59.101
```

Note: Replace the ip with your ip address



In our minikube cluster, the master node is automatically created when we create the cluster.\
So we can see container required for master node like kube-proxy, api service, scheduler etc.

To check running container inside minikube

```
docker ps
// Remainber docker is a default container runtime for kubernetes
```

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

After entering docker ps you will see different kubernete services are running like kube proxy, apiserver, scheduler etc.



### Kubectl commands

Exit the minikube container if you are login.

To get the cluster information&#x20;

```
kubectl cluster-info
```

To get node information

```
kubectl get nodes
```

To get the pod information

```
kubectl get pods
```

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

To list all namespaces avialable in kubectl server

```
kubectl get namespaces
```

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

To check which pods are running inside our namespaces

```
kubectl get pods --namespace=kube-system
```

### To create pod

```
kubectl run nginx --image=nginx
```

It will pull the nginx image from the docker

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

It takes time to pull nginx image from docker

To get more details of the pod

```
kubectl describe pod nginx
```

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

This are the logs how container is created inside pod

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

You can go back to the minikube virtual machine and see the container.

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

Pause container are created to keep namespaces in kubernetes pod share namespaces.



To enter into nginx container

```
docker exec -it a6e7b2b27218 sh
```

To check ip address of container

```
 hostname -i
```

You can also see this ip address outside of the container

```
kubectl get pods -o wide
```

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

10.244.0.3 is a internal ip address of a container so cannot connect through outside world.

So this is how we create container inside pods and pull image in a container.

kubectl command is not convenient because you can only create one pods

Right now, we have created only single pod we cannot increase the quantity of pods using kubectl run command.

To increase the scaling of pod and deploye our application we will learn about deployement.

### To delete pods

```
kubectl delete pod nginx
```

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Now this pod is deleted include the namespace and volume connected to this pod



### Extra

**Try to update your active context of docker which Minikube will pick up.**

```yaml
docker context use default
```

If you are not able to login through ssh try this command

```
ssh-keygen -R <ip_address>
```

