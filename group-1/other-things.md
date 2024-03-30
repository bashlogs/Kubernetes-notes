# Other Things

```
kubectl create ns multitenant

kubectl get namespaces

kubectl -n multitenant create deployment mainapp --image=nginx

kubectl -n multitenant expose deployment mainapp --name=shopping --type=NodePort --port=80

kubectl exec -it secondapp -c busy -- sh
```
