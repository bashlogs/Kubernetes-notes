# Basic Commands

```
kubectl create deployment design2 --image=nginx
kubectl get deployments.apps design2 -o wide
kubectl get deploy -o wide
kubectl get -l app=design2 pod
kubectl get --selector app=design2 pod  -o yaml
kubectl edit pod design2-7b8c799657-822pf
```

