# Basic Troubleshooting

### Basic Troubleshooting Steps <a href="#basic-troubleshooting-steps" id="basic-troubleshooting-steps"></a>

The troubleshooting flow should start with the obvious. If there are errors from the command line, investigate them first. The symptoms of the issue will probably determine the next step to check. Working from the application running inside a container to the cluster as a whole may be a good idea. The application may have a shell you can use, for example:

```
kubectl create deployment troubleshoot --image=nginx
kubectl exec -ti troubleshoot- -- /bin/sh
```

If the Pod is running, use **kubectl logs pod-name** to view the standard out of the container. Without logs, you may consider deploying a **sidecar** container in the Pod to generate and handle logging. The next place to check is networking, including DNS, firewalls and general connectivity, using standard Linux commands and tools.

### Troubleshooting Flow <a href="#troubleshooting-flow" id="troubleshooting-flow"></a>

1. Pods
2. Network and Security
3. Agents

#### Troubleshooting a Pod <a href="#troubleshooting-a-pod" id="troubleshooting-a-pod"></a>

To handle error in pod you have to run it and solve basic syntax, label and selector error
