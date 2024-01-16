---
description: >-
  Config Maps and Secrets in Kubernetes are used to manage configuration data
  and sensitive information, respectively, in a decoupled and portable manner.
---

# Config Maps and Secrets

## Config Maps

* **Purpose:** To store non-sensitive configuration data, such as environment variables, configuration files, or command-line arguments.
* **Use Case:** ConfigMaps help in separating configuration from application code, making it easier to update configurations without modifying the application itself.
* **Benefits:** Centralized management of configuration data, easy updates without changing application code, and better portability across different environments.



{% tabs %}
{% tab title="nginx-cm.yml" %}
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

{% tab title="nginx-deploy.yml" %}
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

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

We can go inside the file and see if the configuration applied or not

```yaml
Command - kubectl exec -it <pod_name> -- /bin/bash
```

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Let's see if the configuration successfully applied or not by creating service for nginx

{% code title="nginx-svc.yml" %}
```yaml
apiVersion: v1
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

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Now go inside the container and create a index.html file and add some content.

```
Commands:

kubectl exec -it nginx-http-7874b58dbc-vnm2n -- /bin/bash

# To install vim:
    apt-get update && apt-get install vim curl -y 

cd /usr/share/nginx/html/
vi index.html
```

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Both configuration applied to the pods.\
First directly access to the index.html file and second 401 error

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

## Secrets

* **Purpose:** To store sensitive information like passwords, API keys, or any confidential data.
* **Use Case:** Secrets provide a secure way to handle sensitive data, ensuring that it is not exposed in the container images or configuration files.
* **Benefits:** Enhanced security by isolating sensitive information, easy updates without changing application code, and support for various sources like environment variables or mounted volumes.

The secrets work like the config maps but the values inside the secrets are obfuscated with the base64.&#x20;

Secrets can be used to store password, tokens, certificates etc.

{% tabs %}
{% tab title="mysql-deploy.yml" %}
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
spec:
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:5.6
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-secret
              key: root-pass
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"

        ports:
        - containerPort: 3306

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

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>









