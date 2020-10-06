```
theia@theiadocker-aalsalih2:/home/project$ docker --version
```
Docker version 18.09.7, build 2d0083d

```
theia@theiadocker-aalsalih2:/home/project$ ibmcloud version
```

ibmcloud version 1.1.0+cc908fe-2020-04-29T04:06:12+00:00
9
git clone https://gitlab.com/ibm/skills-network/courses/cc201.git
cd cc201/labs/1_ContainersAndDocker/
```
docker pull hello-world
docker run hello-world
docker ps -a
docker container rm <container_id>
docker build . -t myimage:v1
docker run -p 8080:8080 myimage:v1
docker stop $(docker ps -q)
exit
```
ibmcloud login
ibmcloud target
ibmcloud cr namespaces
ibmcloud cr region-set us-south
ibmcloud cr login

`Export your namespace as an environment variable so that it can be used in subsequent commands. Make sure to substitute your namespace after the equals sign. If you don't remember your namespace, run ibmcloud cr namespaces. Since you're now logged into your personal account, you should see your personal namespace instead of the one in the lab account.`

```
export MY_NAMESPACE=ahmedibmrg
```
```
docker tag myimage:v1 us.icr.io/$MY_NAMESPACE/hello-world:1
```

Push the newly tagged image to IBM Cloud Container Registry.
```
docker push us.icr.io/$MY_NAMESPACE/hello-world:1
```

Verify that the image was successfully pushed by listing images in Container Registry.
```
ibmcloud cr images
```
`ibmcloud login --apikey $IBMCLOUD_API_KEY

