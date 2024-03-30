# Dockerfile

Create a directory to hold application files. The **docker build** process will pull everything in the directory when it creates the image. Move the scripts and files for the containerized application into the directory.

First build a dockerfile to your application for ex.

{% code title="Dockerfile" %}
```yaml
FROM node:alpine

WORKDIR /usr/src/app

COPY package* ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "index.js"]
```
{% endcode %}

### Build the docker image

```
sudo docker build -t simpleapp:1.0
```

### Verify the image

```
sudo docker images
```

### Run the image

```
sudo docker run simpleapp:1.0
```

### Push the image in dockerhub with tag

```
sudo docker push myusername/simpleapp:1.0
```
