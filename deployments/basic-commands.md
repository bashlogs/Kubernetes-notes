# Basic Commands

### To create a basic deployment from existing image

```
kubectl create deployment design2 --image=nginx
```

### To get all the deployments

```
kubectl get deployments.apps design2 -o wide
kubectl get deploy -o wide
```

### To get the pod with deployment label

```
kubectl get -l app=design2 pod
kubectl get --selector app=design2 pod  -o yaml
```

### To edit the deploy / pods

```
kubectl edit pod design2-7b8c799657-822pf
```
