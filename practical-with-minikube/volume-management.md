# Volume Management

Think of a pod in Kubernetes like a small workspace for your apps. Now, if something goes wrong, and this workspace (pod) crashes, there's a risk of losing data. That's where volumes come in. Volumes act like a safe storage space. So, even if the workspace crashes, your important data stays safe and can be recovered when needed. It's like having a backup for your work, making things more secure and reliable.

The Pod in the Kubernetes cluster can not store the data permanently. Data created inside the Pod will be deleted when the Pod restarts or Pod is deleted. In order to store the data permanently, we need to use the storage object in the **Kubernetes** cluster. Say for example you created an application using Pod. And the application had a **file upload feature**. The uploaded file in the Pod will be deleted when the **Pod restarts** or is **deleted**. So you will **lose** the data.

Kubernetes offers storage components to avoid data loss. Kubernetes had many components for storage such as **Volume, Persistent Volume, Persistent Volume Claim, and Storage Class.** In this tutorial, you will learn what is volume in the Kubernetes cluster and how to create the volume. And also how to attach the volume to the Pod.



### Stateless Applications

* No persistence storage
* Microservice
* APIs
* Helper container
* etc.

### Stateful Applications

* Need persistence storage to functions
* databases
* web servers
* etc.



### Local Volume

{% tabs %}
{% tab title="local-web.yml" %}
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: local-web
spec:
  replicas: 3
  selector:
    matchLabels:
      app: local-web
  template:
    metadata:
      labels:
        app: local-web
    spec:
      containers:
      - name: local-web
        image: nginx
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - name: web
          containerPort: 80
        volumeMounts:
        - name: local
          mountPath: /usr/share/nginx/html
      volumes:
      - name: local
        hostPath: 
          path: /var/nginxserver
```
{% endtab %}
{% endtabs %}

### Deploy the application

```
kubectl apply -f .\local-web.yml
```

#### Make some changes to the index.html file

```
kubectl exec -it <pod name> -- /bin/bash
cd /usr/share/nginx/html/
echo "Hello World" > default.html
ls -l
```

Now we have made some changes in /usr/share/nginx/html/ Now delete the container and recreate it again

```css
kubectl delete deploy local-web
kubectl apply -f .\local-web.yml
```

Now check the changes

```css
kubectl exec -it <pod name> -- /bin/bash
ls /usr/share/nginx/html/
```

**Drawbacks**:- This is the way to create a local storage but this storage is not shared with other nodes. Some application need to shared data across nodes. That why we need a NFS storage or cloud storage to talk to each other.

### Persistence volume

A Persistent Volume represents a piece of storage in the cluster. It could be a physical disk on a node, a network-attached storage device, or any other form of storage. PVs are provisioned by the cluster administrator and are made available for applications to use.

### Persistence volume claim

A Persistent Volume Claim is a request for storage by a user or a pod. It acts as a request for a specific amount of storage with particular access modes (e.g., ReadWriteOnce, ReadOnlyMany, ReadWriteMany). A PVC is used by applications to consume storage without needing to know the details about the underlying storage infrastructure.

### NFS (Storage Class)

Create a nfs server in linux

{% embed url="https://www.redhat.com/sysadmin/nfs-server-client" %}

{% tabs %}
{% tab title="nfs-pv.yml" %}
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfs
spec:
  capacity:
    storage: 500Mi
  accessModes:
    - ReadWriteMany
  storageClassName: nfs
  nfs:
    path: "/srv/nfs"
    server: 192.168.0.110
```
{% endtab %}

{% tab title="nfs-pvc.yml" %}
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfs
spec:
  resources:
    requests:
      storage: 100Mi
  accessModes:
    - ReadWriteMany
```
{% endtab %}
{% endtabs %}

Run the nfs-pv.yml file

```
kubectl apply -f nfs-pv.yml
```

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

We have created the persistence volume now it's time to claim those persistence.

```
kubectl apply -f nfs-pvc.yml
```

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

pvc is successfully bound by pv.

Let's create the deployment for nfs

{% code title="nfs-web.yml" fullWidth="false" %}
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nfs-web
spec:
  replica: 1
  selector:
    matchLabels:
      app: nfs-web
  template:
    metadata:
      labels:
        app: nfs-web
    spec:
      containers:
      - name: nfs-web
        image: nginx
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - containerPort: 80
        volumeMounts:
        - name: nfs
          mountPath: /usr/share/nginx/html
        volumes:
        - name: nfs
          persistentVolumeClaim:
            claimName: nfs
```
{% endcode %}

Deploy this file\
Now enter into the pod and make changes in html file

**Drawback of using nfs :**\
You have to manually setup the nfs server and since it is outside nodes managing throughput and high downtime is highly difficult.

### Cloud Storage

* Using cloud storage in Kubernetes makes sense because it offers scalability, allowing you to easily adjust storage capacity as your application grows.&#x20;
* It provides flexible storage options, ensuring you can choose the right type for your needs.&#x20;
* Cloud storage platforms come with built-in redundancy and data durability, ensuring high availability and protection against data loss.&#x20;
* Features like snapshots and backups simplify data protection, and integration with other cloud services streamlines operations.&#x20;
* With a pay-as-you-go model, it's cost-efficient, and the managed service nature reduces the operational burden, letting your team focus on application development.
* Overall, cloud storage brings simplicity, reliability, and cost-effectiveness to Kubernetes volume management.



### Extra Links

{% embed url="https://medium.com/codex/kubernetes-volume-explained-b346400b9754" %}

[https://www.youtube.com/watch?v=pumX2Ds5L0c](https://www.youtube.com/watch?v=pumX2Ds5L0c)
