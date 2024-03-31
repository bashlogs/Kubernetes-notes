# PV and PVC

## Persistent Volumes and Claims

A **PersistentVolume** (PV) is a storage abstraction used to retain data longer than the Pod using it. Pods define a volume of type **PersistentVolumeClaim** (PVC) with various parameters for size and possibly the type of backend storage known as its **StorageClass**. The cluster then attaches the **PersistentVolume**.

Kubernetes will dynamically use volumes that are available, irrespective of its storage type, allowing claims to any backend storage.

```
$ kubectl get pv
$ kubectl get pvc
```

### Phases of persistence storage

**Provisioning**

Provisioning can be from PVs created in advance by the cluster administrator, or requested from a dynamic source, such as the cloud provider.

**Binding**

Binding occurs when a control loop on the master notices the PVC, containing an amount of storage, access request, and optionally, a particular StorageClass. The watcher locates a matching PV or waits for the StorageClass provisioner to create one. The PV must match at least the storage amount requested, but may provide more.

**Using**

The use phase begins when the bound volume is mounted for the Pod to use, which continues as long as the Pod requires.

**Releasing**

Releasing happens when the Pod is done with the volume and an API request is sent, deleting the PVC. The volume remains in the state from when the claim is deleted until available to a new claim. The resident data remains depending on the **persistentVolumeReclaimPolicy**.

**Reclaiming**

The reclaim phase has three options:

* Retain, which keeps the data intact, allowing for an administrator to handle the storage and data.
* Delete tells the volume plugin to delete the API object, as well as the storage behind it.
* The Recycle option runs an **rm -rf /mountpoint** and then makes it available to a new claim. With the stability of dynamic provisioning, the Recycle option is planned to be deprecated.

## Persistent Volume

The following example shows a basic declaration of a **PersistentVolume** using the **hostPath** type.

{% code title="pv.yaml" %}
```yaml
kind: PersistentVolume
apiVersion: v1
metadata:
name: 10Gpv01
labels:
type: local
spec:
capacity:
        storage: 10Gi
    accessModes:
        - ReadWriteOnce
    persistentVolumeReclaimPolicy: Retain
    storageClassName: maunal
    hostPath:
        path: "/somepath/data01"
```
{% endcode %}

Each type will have its own configuration settings. For example, an already created Ceph or GCE Persistent Disk would not need to be configured, but could be claimed from the provider.

Persistent volumes are cluster-scoped, but persistent volume claims are namespace-scoped. An alpha feature since v1.11 this allows for static provisioning of Raw Block Volumes, which currently support the Fibre Channel plugin. There is a lot of development and change in this area, with plugins adding dynamic provisioning.

## Persistent Volume Claim

{% code title="pvc.yaml" %}
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
  storageClassName: manual
```
{% endcode %}

Create both the files

```
kubectl create -f pv.yaml
kubectl create -f pvc.yaml
```

## Claim as volume

{% code title="nginx.yaml" %}
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  initContainers:
    - name: busybox
      image: busybox
      command: ['sh', '-c', 'echo Hello World! > /usr/share/nginx/html/index.html']
      volumeMounts:
      - mountPath: "/usr/share/nginx/html"
        name: mypod
  containers:
    - name: nginx
      image: nginx
      volumeMounts:
      - mountPath: "/usr/share/nginx/html"
        name: mypod
  volumes:
    - name: mypod
      persistentVolumeClaim:
        claimName: myclaim
```
{% endcode %}

Create the pod and test the connection

```
kubectl create -f nginx.yaml

# Get the pod info.
kubectl get pods -o wide

# Get the pod ip and check the connection
curl <ip_address>
```
