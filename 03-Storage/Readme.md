# Kubernetes Storage
## Working with Host Path
* Create Deployment and PVC
```bash
kubectl apply -f mongo.yaml
kubectl apply -f pvc.yaml
```

* Get PV and PVC
```bash
kubectl get pv,pvc
```

## Working with Azure File
* kubectl exec to check the contents of a file:
    ```bash
    kubectl exec deployment/pwsh-azurefiles -- pwsh -Command Get-Content /mnt/azurefiles/date.txt
    ```

* Add the Azure Files CSI driver to an existing cluster:

    ```bash
    az aks update --name $AKS --resource-group $RG --enable-file-driver
    ```

* List storage classes:
    ```bash
    kubectl get storageclass
    ```