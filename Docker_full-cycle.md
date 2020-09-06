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
```java
docker build -t <new-image-name> .
```
------------------------------------------------
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
> rmi will not work because its running
# Remove the running container
```java
$ docker stop <NAMES>
$ docker rm <NAMES>
```
### Remove image
```java
$ docker rmi <IMAGE ID>
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
nisepidine and latitain cream 4:29PM  4-29


power bi vs alteryx
how does alteryx process data
ventures
cdw data warehouse
fiona DATA LAKE



