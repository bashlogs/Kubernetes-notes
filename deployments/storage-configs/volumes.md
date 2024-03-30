# Volumes

### What is volumes

A Pod specification can declare one or more volumes and where they are made available. Each requires a name, a type, and a mount point.

Keeping acquired data or ingesting it into other containers is a common task, typically requiring the use of a **PersistentVolumeClaim** (pvc).

A particular **access mode** is part of a Pod request. As a request, the user may be granted more, but not less access, though a direct match is attempted first. The cluster groups volumes with the same mode together, then sorts volumes by size, from smallest to largest. The claim is checked against each in that access mode group, until a volume of sufficient size matches.&#x20;

The three access modes are RWO (ReadWriteOnce), which allows read-write by a single node, ROX (ReadOnlyMany), which allows read-only by multiple nodes, and RWX (ReadWriteMany), which allows read-write by many nodes.



### Volume Spec

One of the many types of storage available is an **emptyDir**. The kubelet will create the directory in the container, but not mount any storage. Any data created is written to the shared container space. As a result, it would not be persistent storage. When the Pod is destroyed, the directory would be deleted along with the container.

```
apiVersion: v1
kind: Pod
metadata:
    name: busybox
    namespace: default
spec:
    containers:
    - image: busybox
      name: busy
      command:
        - sleep
        - "3600"
      volumeMounts:
      - mountPath: /scratch
        name: scratch-volume
    volumes:
    - name: scratch-volume
            emptyDir: {}
```

The YAML file above would create a Pod with a single container with a volume named **scratch-volume** created, which would create the **/scratch** directory inside the container.



### Volume Types

**1) GCEpersistentDisk and awsElasticBlockStore**

In GCE or AWS, you can use volumes of type **GCEpersistentDisk** or **awsElasticBlockStore**, which allows you to mount GCE and EBS disks in your Pods, assuming you have already set up accounts and privileges.



**2) emptyDir and hostPath**

**emptyDir** and **hostPath** volumes are easy to use. As mentioned, **emptyDir** is an empty directory that gets erased when the Pod dies, but is recreated when the container restarts. The **hostPath** volume mounts a resource from the host node filesystem.&#x20;



**3) NFS and iSCSI**

**NFS** (Network File System) and **iSCSI** (Internet Small Computer System Interface) are straightforward choices for multiple readers scenarios.



**4) rbd, CephFS and GlusterFS**

**rbd** for block storage or **CephFS** and **GlusterFS**, if available in your Kubernetes cluster, can be a good choice for multiple writer needs.



**5) Others**

Besides the volume types we just mentioned, there are many other possible, with more being added: **azureDisk**, **azureFile**, **csi**, **downwardAPI**, **fc** (fibre channel), **flocker**, **gitRepo**, **local**, **projected**, **portworxVolume**, **quobyte**, **scaleIO**, **secret**, **storageos**, **vsphereVolume**, **persistentVolumeClaim**, etc.​



