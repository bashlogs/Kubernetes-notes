# Security Context

{% tabs %}
{% tab title="Second.yaml" %}


```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secondapp
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - name: busy 
    image: busybox
    command:
      - sleep
      - "3600"
    securityContext:
      runAsUser: 2000
      allowPrivilegeEscalation: false
```

Run Commands

```
kubectl create -f second.yaml
kubectl get pods secondapp -o yaml
kubectl exec -it secondapp -- sh
    ps aux
    grep Cap /proc/1/status
    
capsh --decode=00000000a80425fb
```

Output

{% code overflow="wrap" %}
```
┌──(root💀lulz-AngleCamera)-[~]
└─# capsh --decode=00000000a80425fb
0x00000000a80425fb=cap_chown,cap_dac_override,cap_fowner,cap_fsetid,cap_kill,cap_setgid,cap_setuid,cap_setpcap,cap_net_bind_service,cap_net_raw,cap_sys_chroot,cap_mknod,cap_audit_write,cap_setfcap
```
{% endcode %}
{% endtab %}

{% tab title="Second Tab" %}


```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secondapp
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - name: busy 
    image: busybox
    command:
      - sleep
      - "3600"
    securityContext:
      runAsUser: 2000
      allowPrivilegeEscalation: false 
      capabilities:
        add: ["NET_ADMIN", "SYS_TIME"]
```

Commands

```
kubectl create -f second.yaml
kubectl exec -it secondapp -- sh
    grep Cap /proc/1/status
    
capsh --decode=00000000aa0435fb
```

Ouput

{% code overflow="wrap" %}
```
┌──(root💀lulz-AngleCamera)-[~]
└─# capsh --decode=00000000aa0435fb
0x00000000aa0435fb=cap_chown,cap_dac_override,cap_fowner,cap_fsetid,cap_kill,cap_setgid,cap_setuid,cap_setpcap,cap_net_bind_service,cap_net_admin,cap_net_raw,cap_sys_chroot,cap_sys_time,cap_mknod,cap_audit_write,cap_setfcap
```
{% endcode %}
{% endtab %}
{% endtabs %}
