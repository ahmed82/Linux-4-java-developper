
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
