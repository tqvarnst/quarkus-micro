# Building a Red Hat build of Quarkus minimal image

The purpose of this repo is to show an example on how one can build minimal versions of Quarkus.

This is an example project on how to build a minimal image based on Red Hat build of Quarkus. Note that even if we are using productized version of Red Hat build and a productized version of Mandrel. This example does however use UPX which is not a Red Hat supported component.


## Requirements

To compile and run this demo you will need:

- JDK 11
- Docker machine or Podman

## Clone this repo

> git clone https://github.com/tqvarnst/quarkus-micro && cd quarkus-micro


## Building the application

Build the Quarkus application as a Linux native binary:

> ./mvnw package -Pnative -Dquarkus.native.container-build=true

## Build the container

> docker build -f src/main/docker/quarkus-micro -t quarkus-micro .

## Run the container

> docker run -it --rm -p 8080:8080 quarkus-micro

# Conclusion

The resulting image should be around 40MB compared to around 100MB using UBI minimal and uncompressed Quarkus.
