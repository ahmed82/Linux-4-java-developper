# Az login
`
loudName": "AzureCloud",
"homeTenantId": "a6b169f1-592b-4329-8f33-8db8903003c7",
"id": "5d5922ed-d956-4fc6-8321-a23bb580a577",
"isDefault": false,
"managedByTenants": [
{
"tenantId": "2f4a9838-26b7-47ee-be60-ccc1fdec5953"
}

    Please set this to true
    and then do az login
    get credentials
    and try it
    This cloud is configured on dev subscription
    
5d5922ed-d956-4fc6-8321-a23bb580a577
    So you need to make this one as default 
    "isDefault":true
`
## set defult subsecription
```
az account set --subscription XXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXX
```
## list subsecription
```
as account list --output table
```
```
az aks get-credentials --resource-group $rg --name $aks --overwrite-existing
```
```
kubectl config set-context --current --namespace=$ns
```
```
az acr login --name $acr
```
```
helm get values gf-bot-qa -o yaml > gf.values.yml
```
# Azure Maven deploy plugin
```
mvn com.microsoft.azure:azure-webapp-maven-plugin:1.12.0:config
```


## Life log app service
```
tail -f LogFiles/Application/spring.RD501AC53AC551.log
```
or
```
watch tail -n20 your.log

less +F file.log
```
The benefit is that less can also truncate long lines for you with the -S flag, preventing them from wrapping around the terminal screen while allowing you to scroll left/right.
Instead of piping tail -f file.log through cut or something similar, you can just:
```
less -S +F file.log
```


# System Property
```
[user@host ~]$ java -jar -Dspring.profiles.active=test myproject.jar
```

## Program Argument
```
[user@host ~]$ java -jar myproject.jar --spring.profiles.active=test
```

---


# System environment Variable:

## Windows: Start -> type "envi" select environment variables and add a new: 
Name: spring_profiles_active
Value: dev (or whatever yours is)

## Linux: add following line to /etc/environment under PATH:

spring_profiles_active=prod (or whatever profile is)

then also export spring_profiles_active=prod so you have it in the runtime now.

#### OR

# For Tomcat 8:

## Linux :

Create setenv.sh and update it with following:

export SPRING_PROFILES_ACTIVE=dev

## Windows:

Create setenv.bat and update it with following:

set SPRING_PROFILES_ACTIVE=dev
