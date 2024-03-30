# Minikube

## Let's start the minikube <a href="#lets-start-the-minikube" id="lets-start-the-minikube"></a>

Command:

```
minikube start --driver=<virtual machine name>
```

### For Virtualbox:

```
minikube start --driver=virtualbox --no-vtx-check

// Personal Configurations
minikube start --driver=virtualbox --memory 4000 --cpus 4 --no-vtx-check
```

### For Docker

```
minikube start --driver=docker
```

### For Hyper-v, hyperkit, parallels, vmware

Copy

```
minikube start --driver=hyperv
minikube start --driver=hyperkit
minikube start --driver=parallels
minikube start --driver=vmware
```

After Installation check the status:

```
minikube status
```

![](https://bashlogs.gitbook.io/\~gitbook/image?url=https:%2F%2Fcontent.gitbook.com%2Fcontent%2FuAu6jYJqhZp7YpOWRmwI%2Fblobs%2FumlZeWRP4SPQuP3MGvTH%2Fimage.png\&width=768\&dpr=4\&quality=100\&sign=71304331ff2aa19c2871b55547712ba59e7ef10763a9d2fd2e24f197635853d1)

![](https://bashlogs.gitbook.io/\~gitbook/image?url=https:%2F%2Fcontent.gitbook.com%2Fcontent%2FuAu6jYJqhZp7YpOWRmwI%2Fblobs%2FIEdiw7qU80GtZueaxfFa%2FVirtualBox\_JUDYAdqQTJ.png\&width=768\&dpr=4\&quality=100\&sign=e9e20111d1c8fa21da3860d533b2b910794c1d40a32b4af69b0a9398e05a676c)

That's it, a single node cluster is successfully created in your machine.
