# Config Maps

```
kubectl create configmap colors \
--from-literal=text=black \
--from-file=./favorite \
--from-file=./primary/
```

## Config Maps and Secrets

Config Maps and Secrets in Kubernetes are used to manage configuration data and sensitive information, respectively, in a decoupled and portable manner.

### Config Maps <a href="#config-maps" id="config-maps"></a>

* **Purpose:** To store non-sensitive configuration data, such as environment variables, configuration files, or command-line arguments.
* **Use Case:** ConfigMaps help in separating configuration from application code, making it easier to update configurations without modifying the application itself.
* **Benefits:** Centralized management of configuration data, easy updates without changing application code, and better portability across different environments.

nginx-cm.ymlnginx-deploy.ymlCopy

{% tabs %}
{% tab title="nginx-cm.yaml" %}
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-cm
data:
  # key: value
  nginx.conf: |
    user nginx;
    worker_processes 1;
    events {
      worker_connections  10240;
    }
    http {
      server {
        listen       80;
        server_name  _;
        location / {
          root   /usr/share/nginx/html;
          index  index.html index.htm;
        }
        location /test {
          return 401;
        }
      }
    }
```
{% endtab %}

{% tab title="nginx-deploy.yaml" %}
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-http
spec:
  selector:
    matchLabels:
      app: nginx-http
  template:
    metadata:
      labels:
        app: nginx-http
    spec:
      containers:
      - name: nginx-http
        image: nginx
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - name: web
          containerPort: 80
        volumeMounts:
        - name: nginx-cm
          mountPath: /etc/nginx
        - name: nginx-http-vol
          mountPath: /usr/share/nginx/html
      volumes:
      - name: nginx-cm
        configMap:
          name: nginx-cm
      - name: nginx-http-vol
        hostPath:
          path: /var/nginxserver
```
{% endtab %}
{% endtabs %}

Run nginx-cm.yml file first and the run the nginx.deploy.yml file

```
kubectl apply -f .\configMaps\nginx-cm.yml
kubectl apply -f .\configMaps\nginx-deploy.yml
```

![](https://bashlogs.gitbook.io/\~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252F1RNXh3OBmP3XaqOGIySw%252Fimage.png%3Falt=media%26token=763e1384-5b79-4fa9-a5cc-94038bbbcc35\&width=768\&dpr=4\&quality=100\&sign=b50cd958ba4e6889737cad92dfb58e71f557ab2bb8750f56e60df34b5fafb500)

We can go inside the file and see if the configuration applied or not

```
Command - kubectl exec -it <pod_name> -- /bin/bash
```

![](https://bashlogs.gitbook.io/\~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252F5ugRhiCIBVFo6X6zVaI9%252Fimage.png%3Falt=media%26token=078a84c0-e697-45a5-a31f-919704e8b798\&width=768\&dpr=4\&quality=100\&sign=c4bc90d5cf7cce8be2c3486fc0128655ce292efe6179a2bedc26122695cdb06c)

Let's see if the configuration successfully applied or not by creating service for nginx

{% code title="nginx-svc.yml" %}
```yaml
ExplainapiVersion: v1
kind: Service
metadata:
  name: nginx-http-svc
  labels:
    app: nginx-http
spec:
  type: LoadBalancer
  ports:
  - port: 30080
    targetPort: 80
    protocol: TCP
    name: http
  selector:
    app: nginx-http
```
{% endcode %}

![](https://bashlogs.gitbook.io/\~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252FwwE99J0zpjaYVhnlZG2M%252Fimage.png%3Falt=media%26token=04809bee-3ebe-410c-9a1e-d505c8fafcb8\&width=768\&dpr=4\&quality=100\&sign=e6ff3b7f3c386e2f2ca23e464d714554cb7149f4d461fae795a47ee506a47991)

Now go inside the container and create a index.html file and add some content.

```yaml
ExplainCommands:

kubectl exec -it nginx-http-7874b58dbc-vnm2n -- /bin/bash

# To install vim:
    apt-get update && apt-get install vim curl -y 

cd /usr/share/nginx/html/
vi index.html
```

![](https://bashlogs.gitbook.io/\~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252FKNLzvAMYblooX8OWXtkg%252Fimage.png%3Falt=media%26token=eb3a4b4e-195c-47a7-96e1-d6fdb948f774\&width=768\&dpr=4\&quality=100\&sign=02e253b3c4a5502d88ef50bd54a7c791d71f9d315dede59c9028859a82081f1f)

Both configuration applied to the pods. First directly access to the index.html file and second 401 error

![](https://bashlogs.gitbook.io/\~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252F0MotSQBbTKKDQJN2W6xG%252Fimage.png%3Falt=media%26token=57754b06-5327-4258-8a2b-3c99d8e4f288\&width=768\&dpr=4\&quality=100\&sign=393b73f7a81799a925787182f9b832b67545ef6f49e9cf4823ae6dba30e7d8e7)

![](https://bashlogs.gitbook.io/\~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252F4KEZrD8UhbCARsZ9ucGf%252Fimage.png%3Falt=media%26token=edf87132-e784-4fc8-b0f5-ef71558be97e\&width=768\&dpr=4\&quality=100\&sign=b593cdae11df308f7522feb82f13f3885c98002b436eaab3cb1992207bfd694f)

### Secrets <a href="#secrets" id="secrets"></a>

* **Purpose:** To store sensitive information like passwords, API keys, or any confidential data.
* **Use Case:** Secrets provide a secure way to handle sensitive data, ensuring that it is not exposed in the container images or configuration files.
* **Benefits:** Enhanced security by isolating sensitive information, easy updates without changing application code, and support for various sources like environment variables or mounted volumes.

The secrets work like the config maps but the values inside the secrets are obfuscated with the base64.

Secrets can be used to store password, tokens, certificates etc.

{% tabs %}
{% tab title="mysql-deploy.yml" %}
```yaml
ExplainapiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - image: mysql:5.7
        resources:
          limits:
            memory: "512Mi"
            cpu: "1000m"
        name: mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-secret
              key: root-pass
        ports:
        - name: mysql
          containerPort: 3306
```
{% endtab %}

{% tab title="mysql-secret.yml" %}
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
type: Opaque
stringData:
  root-pass: test123
```
{% endtab %}
{% endtabs %}

Run both the files

```
kubectl apply -f .\configMaps\mysql-secret.yml
```

![](https://bashlogs.gitbook.io/\~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252Fr6gH7VksVYtJuWe9NlUM%252Fimage.png%3Falt=media%26token=2b2162db-901b-479f-b462-543609fcd4e8\&width=768\&dpr=4\&quality=100\&sign=15c4d69e2e3aae6964b7d0831a3686d2cc428517d5c6230f451bf4744b0d9ed0)

To Edit the secret file

```
kubectl edit secrets mysql-secret
```

Now the mysql-deploy file

```
kubectl apply -f .\configMaps\mysql-deploy.yml
```

Now to check if the password is successfully applied or not go inside the pod

```
kubectl exec -it mysql-7b9465b6cb-wn7zb -- /bin/bash
```

![](https://bashlogs.gitbook.io/\~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252F4gnrv0Y13yxYG5c8VBRs%252Fimage.png%3Falt=media%26token=3100f7b1-6c0a-488e-9af5-8df8706b6e07\&width=768\&dpr=4\&quality=100\&sign=5f6858e95165c0fa278854b3b8a5003731ae52c48c4b3fddd94d0a760ffc8544)

### Nginx Certificate in a secret[ ](https://bashlogs.gitbook.io/kubernetes/practical-with-minikube/volume-management) <a href="#nginx-certificate-in-a-secret" id="nginx-certificate-in-a-secret"></a>
