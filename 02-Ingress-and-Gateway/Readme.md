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
    kubectl create ingress myapp --rule="/=hello-service:80" --class=webapprouting.kubernetes.azure.com
    ```

    or
    
    ```bash
    kubectl apply -f ingress.yaml
    ```
    
    web is a service name

* Get Ingress
    ```bash
    kubectl get ingress --watch
    ```
