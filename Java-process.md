
# JAVA Process
##view the running java application on server:
```
ps -ef |grep java  
```
## Desiplay only the PID with pip | awk '{ print $2 }'
`ps -ef |grep <java-app-name>  | awk '{ print $2 }'
```
ps -ef |grep license-management  | awk '{ print $2 }'
```
```
pkill -9 -f <nameOfYourJavaAplication>
kill -9 PID
```
