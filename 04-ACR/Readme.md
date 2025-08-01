# Azure Container Registry
## Create ACR
* Set variables used for the sample commands:
    ```bash
    RG=rg-create-an-azure-container-registry
    ACR=cr$RANDOM
    SKU=basic
    ```
    
* Create an Azure Container Registry:
    ```bash
    az acr create \
    --name $ACR \
    --resource-group $RG \
    --sku $SKU
    ```

* Create an AKS cluster with an attached Container Registry:
    ```bash
    az aks create \
    --name NewCluster \
    --resource-group $RG \
    --attach-acr $ACR \
    --generate-ssh-keys
    ```

* Attach a Container Registry to an existing AKS Cluster:
    ```bash
    az aks update \
    --name ExistingCluster \
    --resource-group $RG \
    --attach-acr $ACR
    ```

* Validate an attached Container Registry:
    ```bash
    az aks check-acr \
    --name ExistingCluster \
    --resource-group $RG \
    --acr $ACR
    ```

## Deploy Application
* Set variables used for the sample commands:
    ```bash
    RG=rg-build-and-push-container-images
    ACR=$(az acr list --resource-group $RG --query [].name --output tsv)
    ```
* Log in to an Azure Container Registry (ACR):
    ```bash
    az acr login --name $ACR
    ```
* Clone a Git repository:
    ```bash
    git clone https://github.com/pluralsight-cloud/aks-deploy-applications
    ```
* Build a container image using Docker:
    ```bash
    docker build --tag akswebapp:v1 .
    ```
* Tag an image so it can be pushed to an Azure Container Registry (ACR):
    ```bash
    ACR_LOGIN_SERVER=$(az acr show --name $ACR --query loginServer --output tsv)
    docker tag akswebapp:v1 $ACR_LOGIN_SERVER/akswebapp:v1
    List images with Docker:

    docker image list
    ```

* Push a container image to Azure Container Registry (ACR) using Docker:
    ```bash
    ACR_LOGIN_SERVER=$(az acr show --name $ACR --query loginServer --output tsv)
    docker push $ACR_LOGIN_SERVER/akswebapp:v1
    Build a container image using a quick task in Azure Container Registry (ACR):

    az acr build --registry $ACR --image akswebapp:v1 .
    ```