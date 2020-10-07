
https://kubernetes.io/docs/tasks/tools/install-minikube/
```
kubectl version --client
```

Minikube using Chocolatey
```
choco install minikube
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
