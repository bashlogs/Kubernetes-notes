# Cluster IP

For inter-cluster communication, frontends talking to backends can use ClusterIPs. These addresses and endpoints only work within the cluster.

ClusterIP is the default type of service created.

```yaml
spec:
  clusterIP: 10.108.95.67
  ports:
  - name: "443"
    port: 443
    protocol: TCP
    targetPort: 443
```
