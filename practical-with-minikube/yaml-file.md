# YAML File

Until now, we have created all the service, deployment, replicas using kubectl command.\
But this is not the way to create deployment

We can create configuration of all the things which we needed for deployment in YAML file.\
Then with the apply command we can configure everything in one click



To delete everything you have create

```
kubectl delete all -all
```

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

### YAML Configuration

create 2 file in your project repo

1. deployment.yaml
2. service.yaml

Documentation on how to create this file

{% embed url="https://kubernetes.io/docs/reference/kubernetes-api/" %}

deployment.yaml file

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-hello
spec:
  replicas: 4
  selector:
    matchLabels:
      app: web-hello
  template:
    metadata:
      labels:
        app: web-hello
    spec:
      containers:
      - name: web-hello
        image: bashlogs/web-hello
        resources:
          limits:
            memory: "128Mi"
            cpu: "250m"
        ports:
        - containerPort: 3000
```

Information of all of this is present in the documentation

To deploy the application or to apply the yaml file

```
kubectl apply -f .\deployment.yaml
```

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

service.yaml file

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-hello
spec:
  type: LoadBalancer
  selector:
    app: web-hello
  ports:
  - port: 3030
    targetPort: 3000
  
```

Apply the changes of service.yaml

```
kubectl apply -f service.yaml
```

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

It's easy to delete the deployment also

```
kubectl delete -f deployment.yaml -f service.yaml
```

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

### Two deployment connectivity

1st container: our hello world web application\
2nd container: nginx container

Since to create both deployment file and service file for each container is hard, we can combine deployment and service file into one yaml file

I have update the code in web-to-nginx folder of my github repo

Github repo -&#x20;

For web-hello app:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-to-nginx
spec:
  type: LoadBalancer
  selector:
    app: web-to-nginx
  ports:
  - port: 3333
    targetPort: 3000
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-to-nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-to-nginx
  template:
    metadata:
      labels:
        app: web-to-nginx
    spec:
      containers:
      - name: web-to-nginx
        image: bashlogs/web-to-nginx
        resources:
          limits:
            memory: "128Mi"
            cpu: "250m"
        ports:
        - containerPort: 3000

```

For nginx container:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  selector:
    app: nginx
  ports:
  - port: 80
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 5
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        resources:
          limits:
            memory: "128Mi"
            cpu: "250m"
        ports:
        - containerPort: 80

```

Let's apply both files

```
kubectl apply -f .\web-to-nginx.yaml -f .\nginx.yaml
```

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

After apply the yaml file our application got deployed

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Some of the pods are not running to still we can connect to our application

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>



Here both of the container are running totally fine and they also communicate with each other

Here in the application we expose 2 port one for express and second for nginx\
But since one application is communicating with nginx server there is no need to expose the port with type. we can assign clusterip address to nginx.

Container inside one pod share same namespace so they can communicate with each other.

With the help of the dns lookup we can check the ip of nginx container

```
kubectl exec web-to-nginx-6dfcf89756-g2r7c -- nslookup nginx
```

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

```
 kubectl exec web-to-nginx-6dfcf89756-g2r7c -- wget -qO- http://nginx
```

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>



