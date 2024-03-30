# Kubectl

## Installation

**Recommendation**: minikube comes with kubectl commands but you can't use those commands for other cloud platforms or personal use. So install kubectl and minikube seprately

I am using window machine so i will perform all the installatio operation / command operation according to my window machine.

### [Kubectl](https://kubernetes.io/docs/tasks/tools/) <a href="#kubectl" id="kubectl"></a>

* [Install kubectl on Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux)
* [Install kubectl on macOS](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos)
* [Install kubectl on Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows)

**Window installation using chocolatey:**

```
choco install kubernetes-cli
```

Test to ensure the version you installed is up-to-date:

```
kubectl version --client
```

Navigate to your home directory:

```
# If you're using cmd.exe, run: cd %USERPROFILE%
cd ~
```

Create the `.kube` directory:

```
mkdir .kube
```

Change to the `.kube` directory you just created:

```
cd .kube
```

Configure kubectl to use a remote Kubernetes cluster:

```
New-Item config -type file
```



## After Installing the kubectl install minikube

{% content-ref url="minikube.md" %}
[minikube.md](minikube.md)
{% endcontent-ref %}
