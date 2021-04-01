# Import Certification to JKS 

## Format
```
keytool -importcert -file Federation+53.cer -keystore samlKeystore.jks -alias tamqaws
```
```
keytool -delete -alias tamqaws -keystore boltKeystore.jks -storepass P@assword
keytool -import -alias tamqaws -file Federation.cer -keystore boltKeystore.jks -storepass P@assword -noprompt
keytool -list -keystore boltKeystore.jks -storepass P@assword
```
### Warning:
The JKS keystore uses a proprietary format. It is recommended to migrate to PKCS12 which is an industry standard format using "keytool -importkeystore -srckeystore boltKeystore.jks -destkeystore boltKeystore.jks -deststoretype pkcs12".

```
keytool -importkeystore -srckeystore boltKeystore.jks -destkeystore boltKeystore.jks -deststoretype pkcs12  -storepass P@assword
```
