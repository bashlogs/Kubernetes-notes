# Containerizion

To containerize an application, you begin by creating your application.

The more stateless and transient the application, the better. Also, remove any environmental configuration, as those can be provided using other tools, like ConfigMaps and secrets.

Develop the application until you have a single build artifact which can be deployed to multiple environments without needing to be changed, using decoupled configuration instead.



The use of Docker had been the industry standard. There are other open source tools that companies are switching

1. [Buildah](https://github.com/containers/buildah)
2. [Podman](https://github.com/containers/podman)

