

## external properties file
```
java -jar app.war --spring.config.location=application-qa.yml
java -jar app.war  -Dspring.config.location=application-qa.yml
```

## systemd
```
ExecStart=/opt/legal/license-management.war --spring.profiles.active=qa
```

## Running the War/Jar
```
java -jar app.war --spring.profiles.active=qa
```
```
java -jar -Dspring.profiles.active=dev app.jar
```
```
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

## environment variable
```
SPRING_PROFILES_ACTIVE 
```

You can define them as you did, using -Dspring.profiles.active when running your jar. You can also set the profile using a SPRING_PROFILES_ACTIVE environment variable or a spring.profiles.active system property.

## set env variable Linux
```
export SPRING_PROFILES_ACTIVE=QA
```
```
setx -m JAVA_HOME "C:\Progra~1\Java\jdk1.8.0_XX"
```

### Test Env , in new PowerShell window, type:
```
$env:PATH
```

## make you IDE use specific profile, add in the Run configurations... -> Arguments
```
-Dspring.profiles.active=dev
```
# pass value to the application
## 1 To pass valuse for properties or pom file .. all you need to defign it as 
```
${value}
```
Besides using files, we can pass properties directly on the command line:
```
java -jar app.jar --property="value"
```
## 2 or system properties,  before the -jar command:
```
java -Dproperty.name="value" -jar app.jar
```
## 3 Spring Boot will also detect environment variables, treating them as properties:
```
export name=value
java -jar app.jar
```


