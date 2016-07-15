# SDH CI Harvester Docker

Deploying and executing the __CI Harvester__ of the *Smart Developer Hub* project with Docker.

## Usage instructions

### Building the Docker image

The first step consists in building the image defined by `Dockerfile` in the repository's root directory:

```bash
docker build -t sdh/ci-harvester .
```

### Running the container

In order to run the *CI Harvester* it is necessary to define several environment variables:

* __HTTP_HOST__: the host through which the *CI Harvester* will be available, so that proper dereferenciable URLs are generated. It can be specified using an IP address (*e.g.*, 192.168.99.100) or a the fully qualified domain name (*e.g.*, cih.smartdeveloperhub.org).

* __HTTP_PORT__: the port to be used by the *CI Harvester*. This port will have to be exposed by the container.

* __TARGET__: the Jenkins instance to be used by the *CI Harvester*. The endpoint can be specified using an IP address (*e.g.*, http://192.168.1.33:8080/) or a fully qualified domain name (*e.g.*, http://jenkins.smartdeveloperhub.org:8080/). 

* __BROKER_HOST__: the host in which the *RabbitMQ broker* used by the __Curator__ that the *CI Harvester* leverages for enriching its data is available. Again, the host can be specified as an IP address or a fully qualified domain name.

* __BROKER_PORT [OPTIONAL]__: the port used by the abovementioned RabbitMQ broker.

Taking all of this into account a container could be executed as follows:

```bash
docker run -e "HTTP_HOST=192.168.99.100" \
           -e "HTTP_PORT=8088" \
           -e "TARGET=http://jenkins.smartdeveloperhub.org:8080/" \
           -e "BROKER_HOST=192.168.51.1" \
           -e "BROKER_PORT=12345" \
           -p 8088:8088 \
           --name sdh-ci-harvester
           sdh/ci-harvester
```

### License

SDH-CI-Harvester-Docker is distributed under the Apache License, version 2.0.
