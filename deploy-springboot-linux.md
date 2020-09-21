## Deploy Jar/war to Linux OS

### make the packaged java application excutable
```java
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <configuration>
        <executable>true</executable>
    </configuration>
</plugin>
```

/opt/webapp/application.war

set the log int /var/log/webapp/application-log.log

## Install Java
```java
sudo yum install java-1.8.0-openjdk-devel
```
for JDK 11
```java
yum install java-11-openjdk-devel
```
Verify the installtioin:
```java
rpm -qa | grep 
```
## 1- System V Init
```java
$ sudo ln -s /var/myapp/myapp.jar /etc/init.d/myapp
$ sudo service myapp start
```
` If your application fails to start, check the log file written to /var/log/<appname>.log for errors.
## 2- Java as a Service Systemd
we create a script named your-app.service using the following example and put it in
```java
$ cd /etc/systemd/system
$ vi your-app.service
```
Add:
```java
[Unit]
Description=A Spring Boot application
After=syslog.target
 
[Service]
User=deployment-user
ExecStart=/path/to/your-app.jar 
SuccessExitStatus=143 
 
[Install] 
WantedBy=multi-user.target
```
I made small modifecation to run the war file" if you dont want to change the permission.
```java
ExecStart=/usr/bin/java -jar /opt/legal/license-management.war
```
To avoid using `/usr/bin/java -jar` you should change the war permission `the point to give excute permission.
```java
$ chmod 500 your-app.war
```
## Controlle you java application
```java
$ systemctl daemon-reload
$ systemctl start license-management.service
$ systemctl status license-management.service
```

##	Memory and Environment Configuration
JVM heap size can be maxed at 1000MB.  To do this, set the following environment variable prior to running tomcat’s startup.sh script:
```xml
export JAVA_OPTS="-Xms1024m -Xmx2048m -Dspring.profiles.active=XXX"
```
`Where XXX is one of {dev, qa, prod} that indicates the environment it is deployed to.




