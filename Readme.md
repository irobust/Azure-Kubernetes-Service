# Azure Kubernetes Service (AKS)

## Connect to Azure

**To log into Azure**

```bash
az login --tenant [Tenant ID]
```


**To verify if the correct Azure Subscription is used**

```bash
az account show
```


**To set default resource group**

```bash
az configure --defaults group=aks-rg1
```


**To get AKS credentials**

```bash
az aks get-credentials --name <nameoftheAKSCluster>
```


**To install the Kubectl CLI**

```bash
az aks install-cli
```


**To check the number of nodes**

```bash
kubectl get nodes
```

## Run sample application

**To run the sample application on docker**

```bash
docker container run --name myappv1 --detach -p 8080:80 manojnair/myapp:v1
```

**To check for deployments** 

```bash
kubectl get deployments
```


**To check for Pods**

```bash
kubectl get pods
```


**To create a deployment**

```bash
kubectl create deployment myapp --image=manojnair/myapp:v1 --replicas=1
```

## Scaling application
**To scale a deployment**

```bash
kubectl scale deployment myapp --replicas=10
```


**To expose a deployment as a service**

```bash
kubectl expose deployment myapp --type=LoadBalancer --target-port=80 --port=80
```


**To wait for service creation**

```bash
kubectl get svc --watch
```


**To scale AKS nodes**

```bash
az aks nodepool scale --name <your node pool name> --cluster-name myAKSCluster --resource-group myResourceGroup  --node-count 0
```