After create the 
**Dockerfile**:
```java
FROM openjdk:8-jdk-alpine
EXPOSE 8080
MAINTAINER Ahmed AlSalih
RUN mkdir -p /usr/java/app
WORKDIR /usr/java/app
COPY target/springboot-docker.war /usr/java/app
ENTRYPOINT ["java","-jar","springboot-docker.war"]
```

## Use multi-stage builds
```java
FROM maven:3-jdk-8  AS build
WORKDIR /workspace/app
COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .
COPY src src
RUN mvn install -DskipTests
# RUN ls && pwd && cd target  && ls

FROM openjdk:8-jdk-alpine
RUN mkdir -p /usr/java/app && cd /usr/java/app
WORKDIR /usr/java/app
COPY --from=build /workspace/app/target/license-management.war /usr/java/app
ENTRYPOINT ["java","-jar","license-management.war"]
```
-------------------------------------------------
PID: is just one of the Linux namespaces that provides containers with isolation to system resources. Other Linux namespaces include:
MNT: Mount and unmount directories without affecting other namespaces.
NET: Containers have their own network stack.
IPC: Isolated interprocess communication mechanisms such as message queues.
User: Isolated view of users on the system.
UTC: Set hostname and domain name per container.
These namespaces provide the isolation for containers that allow them to run together securely and without conflict with other containers running on the same system.

## Create Image
```java
docker build -t <new-image-name> .

docker tag myimage:v1 us.icr.io/$MY_NAMESPACE/hello-world:1
docker push us.icr.io/$MY_NAMESPACE/hello-world:1
```
------------------------------------------------
## Run the Image
The -t flag allocates a pseudo-TTY:
```java
docker run -p 91:80 -- name web <imagename>
docker container run --name web -p 66:8080  -it -d spring-boot-docker
```
### list Images
```
docker images
```
### list all containers / running os stoped
```xml
docker ps -a
```
-----------------------------------------------------------------------------------------
### list all the running container
```
docker ps
```
## Stop the containers by running this command for each container in the list:
```
$ docker container stop [container id]
```
`Tip: You need to enter only enough digits of the ID to be unique. Three digits is typically adequate.`

## or Stop and Remove the running container
```java
$ docker stop <NAMES> 
$ docker rm <NAMES>
```
### Remove image
```java
$ docker rmi <IMAGE ID>
```
### Remove All images
```
docker image prune
```
## Remove the stopped containers.
The following command removes any stopped containers, unused volumes and networks, and dangling images:
```
$ docker system prune
```
# Stop & Delete all Containers

## Delete all running and stopped containers
Run This command in Power-Shell
```java
$ docker container rm -f $(docker ps -aq)
```
or 
```java
$ docker stop $(docker ps -aq)
$ docker rm $(docker ps -aq)
```
Then
```java
$ docker rmi <IMAGE ID>
```
----------------------------------------------------------------------------------------
> Go inside container
```java
$ docker exec -it <container-id> /bin/sh
$ winpty docker exec -it <container-id> //bin//sh
```
----------------------------------------------------------------------------------------
## Print the last 100 lines of a container’s logs 
```xml
$ docker container logs --tail 100 web
```
```xml
docker run -d -it --name os ubuntu
```
> -i mean this std is open <Standered Input is Open>
> -t interactive processor 
> -d detached mode / so the process will not be attached to the terminal if closed will killed

```java
docker exec -it os bash
```
os = name of the docker 
bash = command lind inside the docker
```java
mkdir test
exit
```
back to desktop
```java
docker stop os
docker rm os
```
> All the change in the docker container gone

without Dokerfile you can pull
docker pull ubuntu

## Build a Docker Image with Maven
Spring Boot image generator without even changing your pom.xml (and remember the Dockerfile if it is still there is ignored):
```java
$ ./mvnw spring-boot:build-image -Dspring-boot.build-image.imageName=springio/gs-spring-boot-docker
```
## Volumes / bind --mount

docker run -p 8080:8080 -p 50000:50000 -v /your/home:/var/jenkins_home jenkins
## Multi stage dynamic
Parameterized build file. In Docker, parameters can be passed using either the ENV or ARG options. Both are set using the --build-arg option on the command-line.
```
FROM alpine/git as clone
ARG url (1)
WORKDIR /app
RUN git clone ${url} (2)
FROM maven:3.5-jdk-8-alpine as build
ARG project (3)
WORKDIR /app
COPY --from=clone /app/${project} /app
RUN mvn install
FROM openjdk:8-jre-alpine
ARG artifactid
ARG version
ENV artifact ${artifactid}-${version}.jar (4)
WORKDIR /app
COPY --from=build /app/target/${artifact} /app
EXPOSE 8080
CMD ["java -jar ${artifact}"] (5)
```
### Building:
```
docker build --build-arg url=https://github.com/spring-projects/spring-petclinic.git\
  --build-arg project=spring-petclinic\
  --build-arg artifactid=spring-petclinic\
  --build-arg version=1.5.1\
  -t nfrankel/spring-petclinic - < Dockerfile
```

```
EXPOSE 8080
ENTRYPOINT ["sh", "-c"]
CMD ["java -jar ${artifact}"] (5)
```
```
FROM maven:3.5.2-jdk-8-alpine AS MAVEN_TOOL_CHAIN
COPY pom.xml /tmp/
COPY src /tmp/src/
WORKDIR /tmp/
RUN mvn package

FROM tomcat:9.0-jre8-alpine
COPY --from=MAVEN_TOOL_CHAIN /tmp/target/wizard*.war $CATALINA_HOME/webapps/wizard.war

HEALTHCHECK --interval=1m --timeout=3s CMD wget --quiet --tries=1 --spider http://localhost:8080/wizard/ || exit 1
```
```
$ sudo docker run -d -p 80:8080 -p 443:8443 -t spring-boot:1.0
```
# IBM class
An image is the blueprint for spinning up containers. An image is a TAR of a file system, and a container is a file system plus a set of processes running in isolation
```
$ docker container run --detach --publish 8080:80 --name nginx nginx
$ docker container run --detach --publish 8081:27017 --name mongo mongo:3.4
```
$ docker container logs [container id] 
$ docker diff
$ docker image history python-hello-world
### Inspect the container:
```
docker container exec
docker container exec -it 37f bash
docker info
docker commit -m "" -a <repo>
docker node ls
docker service ls
```
nisepidine and latitain cream 4:29PM  4-29
power bi vs alteryx
how does alteryx process data
ventures
cdw data warehouse
fiona DATA LAKE



