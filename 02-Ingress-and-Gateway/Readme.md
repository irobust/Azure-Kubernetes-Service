# Ingress and Gateway
## Demo: Configuring the Application Routing Add-on
* Enable App Routing
    ```bash
    az aks approuting enable --resource-group $RG --name $AKS
    ```

* Get IngressClass
    ```bash
    kubectl get ingressclass
    ```

* Create Ingress Definition
    ```bash
    kubectl create ingress web --rule="/=web:80" --class=webapprouting.kubernetes.azure.com
    ```
    
    web is a service name

* Get Ingress
    ```bash
    kubectl get ingress --watch
    ```
