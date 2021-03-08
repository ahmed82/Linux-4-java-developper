# Enable SSL 

## Create Self-sign cetificate
```
keytool -genkeypair -alias tomcat -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore keystore.p12 -validity 3650
```
## Spring Boot configuration
application.yml
```
server:
 port: 8443
 ssl:
      key-store: classpath:keystore/keystore.p12
      key-store-password: password
      keyStoreType: PKCS12
      keyAlias: tomcat
      enabled: true
```
