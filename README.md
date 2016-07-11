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

* __HTTP_HOST__: the fully qualified domain name to be used by the *CI Harvester*, so that proper dereferenciable URLs are generated. It is worth nothing that this domain name should point to the host where the container is to be run, either directly or via a reverse proxy.

* __HTTP_PORT__: the port to be used by the *CI Harvester*. This port will have to be exposed by the container. 

* __TARGET__: the Jenkins instance to be used by the *CI Harvester*. The endpoint can be specified using an IP address (*e.g.*, http://192.168.1.33:8080/) or a fully qualified domain name (*e.g.*, http://jenkins.smartdeveloperhub.org:8080/). 

Taking all of this into account a container which reuses an external data file could be executed as follows:

```bash
docker run -e "HTTP_HOST=cih.smartdeveloperhub.org" \
           -e "HTTP_PORT=8088" \
           -e "TARGET=http://jenkins.smartdeveloperhub.org:8080/" \ 
           -p 8088:8088 \
           --name sdh-ci-harvester 
           sdh/ci-harvester
```

### License

SDH-CI-Harvester-Docker is distributed under the Apache License, version 2.0.
