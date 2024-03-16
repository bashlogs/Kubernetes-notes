# Installation

**Recommendation**: minikube comes with kubectl commands but you can't use those commands for other cloud platforms or personal use. So install kubectl and minikube seprately

I am using window machine so i will perform all the installatio operation / command operation according to my window machine.

## [Kubectl](https://kubernetes.io/docs/tasks/tools/)

* [Install kubectl on Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux)
* [Install kubectl on macOS](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos)
* [Install kubectl on Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows)

#### Window installation using chocolatey:&#x20;

To install kubectl

```
choco install kubernetes-cli
```

Test to ensure the version you installed is up-to-date:&#x20;

```powershell
kubectl version --client
```

Navigate to your home directory:

```powershell
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

```powershell
New-Item config -type file
```

## [Minikube](https://minikube.sigs.k8s.io/docs/start/)

Installation with chocolety

```shell
choco install minikube
```

## Virtual machine ([Virtualbox](https://www.virtualbox.org/wiki/Downloads))

I am going to use virtualbox in this pratical

To download virtual box: [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)

#### For coding purpose Use [Visual studio code](https://code.visualstudio.com/Download) with kubenetes extension
