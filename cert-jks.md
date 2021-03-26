# Import Certification to JKS 

## Format
```
keytool -importcert -file Federation+53.cer -keystore samlKeystore.jks -alias tamqaws
```
```
keytool -delete -alias tamqaws -keystore boltKeystore.jks -storepass Blu3M0nst#r
keytool -import -alias tamqaws -file Federation.cer -keystore boltKeystore.jks -storepass Blu3M0nst#r -noprompt
keytool -list -keystore boltKeystore.jks -storepass Blu3M0nst#r
```
