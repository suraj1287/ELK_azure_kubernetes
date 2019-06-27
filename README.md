## login to azure:

az login --service-principal -u  xxxx00000-0000-000-xxxx-000xxxxxxxx --password  pass@123 --tenant xxxx00000-0000-000-xxxx-000000000000

## create group:

az group create -l eastus -n myapp-elk

## create kubernetes cluster:

sudo az aks create --resource-group myapp-elk --name myapp-elk-aks --node-count 1 --nodepool-name myappelkaks --node-vm-size Standard_A8_v2 --enable-addons monitoring --enable-addons http_application_routing --service-principal xxxx00000-0000-000-xxxx-000xxxxxxxx --client-secret pass@123 --kubernetes-version 1.11.5

## connect to aks:

sudo az aks get-credentials --resource-group myapp-elk --name myapp-elk-aks --overwrite-existing

## deployment:

sudo kubectl create -f elk.yaml

Note: we have map elk.myapp.ai IP to 173.116.122.24 from ingress controller
To check the kibana dashboard url elk.myapp.ai:80

***command to check status:

sudo kubectl get svc
sudo kubectl get deploy
sudo kubectl get ingress
sudo kubectl get pod

****replace POD_NAME from above command in next command to access the pod:

sudo kubectl exec -it [POD_NAME] -- /bin/bash  
sudo kubectl get  pod -n kube-system
sudo kubectl get svc -n kube-system