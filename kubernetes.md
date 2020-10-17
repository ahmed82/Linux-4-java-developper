
https://kubernetes.io/docs/tasks/tools/install-minikube/
```
kubectl version --client
```
## Minikube
Minikube using Chocolatey
```
choco install minikube
```

### Start a cluster using the docker driver:
```
minikube start --driver=docker
```
To make docker the default driver:
```
minikube config set driver docker
```
```
`Power Shall as admin`
minikube start --vm-driver hyperv  --hyperv-virtual-switch "Primary Virtual Switch"
minikube start --kubernetes-version="v1.10.3" --vm-driver="hyperv" --hyperv-virtual-switch="minikube Switch" --v=9
minikube start --vm-driver="hyperv" --memory=4096 --cpus=4 --hyperv-virtual-switch="minikube" --v=7 --alsologtostderr
kubectl [command] [type] [name] [flag]
kubectl get nodes
kubectl get pods -n kube-system
kubectl run demo --image=ubuntu
kubectl get deployment
kubectl get pods
kubectl get pods <pod-name> -o=yaml
minikube status
minikube stop
```
Some examples of **Kubernetes objects** are Pods, namespaces, Deployments, ConfigMaps, and volumes.
**Namespaces:** key point is that namespaces can be used to provide logical separation of a cluster into virtual clusters.
## Imperative commands
* Quickly create, update, and delete kubernetes objects
* Easiest to learn
* Don't provide an audit trail
* Not very flexible
```
kubectl run nginx --image nginx
```
## Declarative commands
* configuration files define one or more objects
* No operation is specified
* Works on files and directories
* Configuration files define desired state, and kubernetes actualizes that state
* Preferred method for production system.

```
kubectl apply -f nginx/
```
```
kubectl apply -f file.yaml
```
```
az acr import -n xxxxxx2diphpc01acr --source docker.io/library/nginx:latest --image nginx:v1
kubectl apply -f cbacr-ngnix.yaml
```
Use the kubectl CLI
* Create a Kubernetes Pod
* Create a Kubernetes Deployment
* Create a ReplicaSet that maintains a set number of replicas
* Witness Kubernetes load balancing in action

```
kubectl version
```
```
[ ! -d 'cc201' ] && git clone https://gitlab.com/ibm/skills-network/courses/cc201.git
cd cc201/labs/2_IntroKubernetes/
```
Recall that Kubernetes namespaces enable you to virtualize a cluster. You already have access to one namespace in a Kubernetes cluster, and kubectl is already set to target that cluster and namespace.

Let's look at some basic kubectl commands.

1- kubectl requires configuration so that it targets the appropriate cluster. Get cluster information with the following command:
```
kubectl config get-clusters
```
2- A kubectl context is a group of access parameters, including a cluster, a user, and a namespace. View your current context with the following command:
```
kubectl config get-contexts
```
3- List all the Pods in your namespace. If this is a new session for you, you will not see any Pods.
```
kubectl get pods
```

Now it's time to create your first Pod. This Pod will run the hello-world image you built and pushed to IBM Cloud Container Registry in the last lab. As explained in the videos for this module, you can create a Pod imperatively or declaratively. Let's do it imperatively first.

1- Check whether your namespace is still set as an environment variable after the first lab.
```
echo $MY_NAMESPACE
```
2- If it's not set, export your namespace as an environment variable so that it can be used in subsequent commands. Make sure to substitute your namespace after the equals sign. If you don't remember your namespace, run ibmcloud cr namespaces.
```
export MY_NAMESPACE=<my_namespace>
```
Build and push the image.
```
docker build -t us.icr.io/$MY_NAMESPACE/hello-world:1 . && docker push us.icr.io/$MY_NAMESPACE/hello-world:1
```

The **"get"** and **"describe"** commands enable you to do this.
The **"get"** command lists one or many resources, while the **"describe"** command shows details about a specific resource or group of resources.
Both commands are namespace-scoped, meaning that by default they will operate on the resources in the targeted namespace.
```
kubectl get pods -o wide
kubectl describe pod <pod_name>
```
Take a look at this output--there's a lot there. If you look closely, you'll notice that there is a ReplicaSet associated with this Pod. This is because the kubectl run command actually created a Deployment with one replica, which in turn created a ReplicaSet. At the end of the output, you'll also see events. These give some history for this resource. For example, you should see events that indicate that this Pod was scheduled, the image was pulled, and the container was started.

7- List the Deployments and ReplicaSets in your namespace to verify that one of each was created.
```
kubectl get deployments,replicasets
```
8- Delete the Deployment. This will also delete the ReplicaSet and the Pod.
```
kubectl delete deployment hello-world
kubectl get pods
```


Imperative object configuration lets you create objects by specifying the action to take (e.g., create, update, delete) while using a configuration file. A configuration file, hello-world-create.yaml, is provided to you in this directory.

Use the Explorer to view and edit the configuration file. Click the Explorer icon (it looks like a sheet of paper) on the left side of the window, and then navigate to the directory for this lab: cc201 > labs > 2_IntroKubernetes. Click hello-world-create.yaml to view the configuration file. Imperative object configuration file in Explorer

Use the Explorer to edit hello-world-create.yaml. You need to insert your namespace where it says <my_namespace>. Make sure to save the file when you're done.

Imperatively create a Pod using the provided configuration file.
```
kubectl create -f hello-world-create.yaml
```
Note that this is indeed imperative, as you explicitly told Kubernetes to create the resources defined in the file.

List the Pods in your namespace.
```
kubectl get pods
```
In this case, kubectl does not create a Deployment for us because the YAML file explicitly defined a Pod.

Delete the Pod.
```
kubectl delete pod hello-world
```
This command can take some time to run.


## Create a Pod with a declarative command
The previous two ways to create a Pod were imperative -- we explicitly told kubectl what to do. While the imperative commands are easy to understand and run, they are not ideal for a production environment. Let's look at declarative commands.

A sample hello-world-apply.yaml file is provided in this directory. Use the Explorer again to open this file. Notice the following:
We are creating a Deployment (kind: Deployment).
There will be three replica Pods for this Deployment (replicas: 3).
The Pods should run the hello-world image (- image: us.icr.io/<my_namespace>/hello-world:1). You can ignore the rest for now. We will get to a lot of those concepts in the next lab.
Use the Explorer to edit hello-world-apply.yaml. You need to insert your namespace where it says <my_namespace>. Make sure to save the file when you're done.

Use the kubectl apply command to set this configuration as the desired state in Kubernetes.
```
kubectl apply -f hello-world-apply.yaml
```
Get the Deployments to ensure that a Deployment was created.
kubectl get deployments
List the Pods to ensure that three replicas exist.
```
kubectl get pods
```
With declarative management, we did not tell Kubernetes which actions to perform. Instead, kubectl inferred that this Deployment needed to be created. If you delete a Pod now, a new one will be created in its place to maintain three replicas.

Note one of the Pod names from the previous step, and delete that Pod.
kubectl delete pod <pod_name>
This command can take some time to run.

List the Pods to see a new one being created.
```
kubectl get pods
```
If you do this quickly enough, you can see one Pod being terminated and another Pod being created.

NAME                    READY   STATUS              RESTARTS   AGE
hello-world-dd6b5d745-2jw5s   0/1     Terminating         0          35s
hello-world-dd6b5d745-f9xjk   1/1     Running             0          35s
hello-world-dd6b5d745-m89fc   0/1     ContainerCreating   0          8s
hello-world-dd6b5d745-qvs9t   1/1     Running             0          35s
Otherwise, the status of each will be the same, but the age of one Pod will be less than the others.

NAME                    READY   STATUS    RESTARTS   AGE
hello-world-dd6b5d745-f9xjk   1/1     Running   0          39s
hello-world-dd6b5d745-m89fc   1/1     Running   0          12s
hello-world-dd6b5d745-qvs9t   1/1     Running   0          39s



## Load balancing the application
Since there are three replicas of this application deployed in the cluster, Kubernetes will load balance requests across these three instances. Let's expose our application to the internet and see how Kubernetes load balances requests.

In order to access the application, we have to expose it to the internet using a Kubernetes Service.
kubectl expose deployment/hello-world --type=NodePort --port=8080 --name=hello-world --target-port=8080
This command creates what is called a NodePort Service. This will open up a port on the worker node to allow the application to be accessed using that port and the IP address of the node.

List Services in order to see that this service was created.
kubectl get services
Two things are needed to access this application: a worker node IP address and the correct port. To get a worker node IP, rerun the get pods command with the wide option and note any one of the node IP addresses (from the column entitled NODE):
```
kubectl get pods -o wide
```
Here is some sample output.

NAME                          READY   STATUS    RESTARTS   AGE   IP               NODE            NOMINATED NODE   READINESS GATES
hello-world-dd6b5d745-f9xjk   1/1     Running   0          7m    172.30.104.185   10.114.85.153   <none>           <none>
hello-world-dd6b5d745-m89fc   1/1     Running   0          7m    172.30.165.182   10.114.85.151   <none>           <none>
hello-world-dd6b5d745-qvs9t   1/1     Running   0          7m    172.30.69.68     10.114.85.172   <none>           <none>
Using this sample output, you could choose 10.114.85.153, 10.114.85.151, or 10.114.85.172 for the node IP address.

Export the node IP address as an environment variable. Make sure to substitute the copied IP address into this command.
```
export NODE_IP=<node_ip>
```
Using the sample output, one correct command would be export NODE_IP=10.114.85.153.

To get the port number, run the following command and note the port:
```
kubectl get services
```
Here is some sample output. In this sample, the port number we need is 31758.

NAME          TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
hello-world   NodePort   172.21.121.84   <none>        8080:31758/TCP   58s
Export the port as an environment variable. Make sure to substitute the copied port into this command.
```
export NODE_PORT=<node_port>
```
Using the sample output, the correct command would be export NODE_PORT=31758.

Ping the application to get a response.
```
curl $NODE_IP:$NODE_PORT
```
Notice that this output includes the Pod name. Run the command ten times and note the different Pod names in each line of output.
for i in `seq 10`; do curl $NODE_IP:$NODE_PORT; done
You should see more than one Pod name, and quite possibly all three Pod names, in the output. This is because Kubernetes load balances the requests across the three replicas, so each request could hit a different instance of our application.

Delete the Deployment and Service. This can be done in a single command by using slashes.
```
kubectl delete deployment/hello-world service/hello-world
```
-----------------------------------------------------------------------
Note that kubectl uses “rs” as a short form for ReplicaSet, because nobody wants
to type more than absolutely necessary! If you already have a deployment that you want
to scale, you can simply use the “scale” command as shown here. The first command creates
a deployment. The second command gets the pods to show it was created. You see the “hello-Kubernetes-longnumber”
```
kubectl get rs
```
pod created. The third command gets the “hello-Kubernetes” deployment. The command after that sets the “replicas” to "3". If you issue another “get pods” command as shown here, you
should see three pods running. The ReplicaSet that was created with the deployment created

If you already have a deployment that you want
to scale, you can simply use the “scale” command as shown here. The first command creates a deployment. The second command gets the pods to show it was created. You see the “hello-Kubernetes-longnumber”
pod created. The third command gets the “hello-Kubernetes” deployment. The command after that sets the
“replicas” to "3". If you issue another “get pods” command as shown here, you
should see three pods running. The ReplicaSet that was created with the deployment created
two more pods, one ending in “flw” and the second ending in “b7v”. How do we
```
kubectl create -f deployment.yaml
```
```
kubectl get pods
```
```
kubectl scal deploy hello-kubernetes --replicas=3
```




