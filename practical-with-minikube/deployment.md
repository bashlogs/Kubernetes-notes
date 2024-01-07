# Deployment

In Kubernetes, deployment refers to the process of managing and scaling applications by defining, deploying, and updating their desired state using declarative configuration.

In Kubernetes, you use a resource called a "Deployment" to declare how applications should run. It includes information such as the container image, the number of replicas, and update strategies.

Deployments allow you to scale your application by adjusting the number of replicas and perform rolling updates to smoothly transition from one version of your application to another.



Difference between deployment and cluster

In cluster you cannot improve the scaling of your application and you can only create one pod in cluster

In deployment you can replicate your application and also increase no. of pods



To create deployment:&#x20;

```
kubectl create deployment nginx-deploy --image=nginx
```

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

To get description / details of our pods

```
kubectl describe deployment nginx-deploy
```

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

This is the description of pods

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

```
Name of deployment: nginx-deploy-d845cc945
Name of the pod: xdk8k
```

Name of the deployment will be as it is since their is only one pod after we create multiple pods the name of pod will get change



To scale our deployment use following command

```
kubectl scale deployment nginx-deploy --replicas=5
```

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

To scale down the deployment size use the same command

```
kubectl scale deployment nginx-deploy --replicas=3
```

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

Right now, we won't be able to connect this pod because pod are running internally in our node.

To establish the connectivity between pods we need to create services.



## Services

In service you can expose specific port to outside world for a deployment

For example, Write now default nginx server is running on port 80 we can expose port 80 from container to outside port 8080

To expose those port use command expose

```
kubectl expose deployment nginx-deploy --port=8080 --target-port=80
```

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

Cluster ip addresses are virtual ip addresses which is create by kubernetes our ip address starts from 172.0.0.1

Cluster ip address is accessible from our minikubes

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

To get information about service

```
kubectl get svc
```

```
kubectl describe service <service_name>
```

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

So far now, We learned about deployment, scaling deployment and services.

Now let's create a custom docker image, push it on docker hub and create deployment of docker image.

To delete deployment and service:

T delete deployment :&#x20;

```
kubectl delete deployment nginx-deploy
```

To delete services :&#x20;

```
kubectl delete service nginx-deploy
```

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

### Creating express node application

Github repo - [https://github.com/bashlogs/Kubernetes](https://github.com/bashlogs/Kubernetes)

I have created a hello world program using express. you can go to link and pull the repo.

Now build your docker image and push it in your docker hub account

To do that first build the image

```
docker build . -t <image_name>
```

Then push it in your docker hub

```
docker push <username>/<image_name>
```

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

Once the image is pushed into docker hub we can deploy our project in minikube



### Deploying the application

```
kubectl create deployment <app_name> --image=<image_name>

For ex..
kubectl create deployment web-hello --image=bashlogs/web-hello
```

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Now let's create service

```
kubectl expose deployment web-hello --port=3000
```

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Now we have create service for our app, you can check it by login into minikube

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Scaling the deployment

```
kubectl scale deployment web-hello --replicas=4
```

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Now if we try to access the service inside minikube, node will automatically give response from different pods. Because it's managing the load between all pods

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Until now, we have created service for internal ip address. let's create the service for external ip address.

You can do that with specifing type to node port

Delete the previous service

```
kubectl delete svc web-hello
```

Create a new service with type nodeport

```
kubectl expose deployment web-hello --type=NodePort --port=3000
```

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Now the external port is created 30627. Now you can connect to your deployment using node ip address

To get the node ip address enter:

```
// Minikube is our node
minikube ip
```

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

if you refresh the website you'll get response from different pod every time

You can also try this command

```
minikube service web-hello
```

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

### Create loadbalancer service

You can also create a loadbalancer service in your kubernetes

Delete the existing service

To create loadbalancer service

```
kubectl expose deployment web-hello --type=LoadBalancer --port=3000
```

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

To get information about deploy application&#x20;

```
kubectl describe deploy web-hello
```

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

Now you can see strategy type rolling update.&#x20;

What is rolling update?

When you release new version of your application you want to roll out this new version in production smoothly without any interruption and kubernete allows that.

When you update the image in node, node will update those image one by one in pods

So for example..\
If there are 4 pods node will update the image sequentially so you might see one pod has update version of app and another pod has previous version. But you won't be able to see this difference because it's happen in matter of seconds



### Let's try to update our app&#x20;

Now we will update our application and give update version name as 2.0 and will see how to modify image in our deployment and how roll out happens in kubernete

I have did little bit change in previous code you can check it out \
Github : [https://github.com/bashlogs/Kubernetes/tree/main/web\_hello2](https://github.com/bashlogs/Kubernetes/tree/main/web\_hello2)

I also build docker image and push it into docker hub\
Docker: [https://hub.docker.com/repository/docker/bashlogs/web-hello/general](https://hub.docker.com/repository/docker/bashlogs/web-hello/general)

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Now let's roll out this 2.0 image in our kubernetes

To set new image on our previous deployed image

```
kubectl set image deployment web-hello web-hello=bashlogs/web-hello:2.0
```

To see how the update happen enter this command

```
kubectl rollout status deploy web-hello
```

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

Here 3 pods where already updated only one pod was remaining for rolling update

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Look at age of the pods old pods got terminated and new pods got created

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

App got updated successfully

