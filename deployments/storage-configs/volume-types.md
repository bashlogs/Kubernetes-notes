# Volume Types

### EmptyDir and HostPath

The following YAML file, for Pod **ExampleA** creates a Pod with two containers, one called **alphacont**, the other called **betacont** both with access to a shared volume called **sharevol**:

```yaml
 containers:
 - name: alphacont
   image: busybox
   volumeMounts:
   - mountPath: /alphadir
     name: sharevol
 - name: betacont
   image: busybox
   volumeMounts:
   - mountPath: /betadir
     name: sharevol
 volumes:
 - name: sharevol
   emptyDir: {}  
    
$ kubectl exec -ti exampleA -c betacont -- touch /betadir/foobar
$ kubectl exec -ti exampleA -c alphacont -- ls -l /alphadir
```

You could use **emptyDir** or **hostPath** easily, since those types do not require any additional setup, and will work in your Kubernetes cluster.

Note that one container wrote, and the other container had immediate access to the data. There is nothing to keep the containers from overwriting the other’s data. Locking or versioning considerations must be part of the application to avoid corruption.



