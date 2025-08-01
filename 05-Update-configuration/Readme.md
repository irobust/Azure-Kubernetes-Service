# Update Configuration Command
## Config Auto Update
```bash
az aks update \
    --resource-group $RG \
    --cluster-name $AKS \
    --auto-update-chanel stable \
    --node-os-upgrade-chanel securitypatch
```

## Set Auto-update NodeOS
```bash
az aks maintenanceconfiguration add \
    --resource-group $RG \
    --cluster-name $AKS \
    --name aksManagedNodeOSUpgradeSchedule \
    --schedule-type weekly \
    --interval-weeks 2 \
    --day-of-week Monday \
    --duration 6 \
    --utc-offset +7:00 \
    --start-time 00:00
```

## Set Auto-update Cluster
```bash
az aks maintenanceconfiguration add \
    --resource-group $RG \
    --cluster-name $AKS \
    --name aksManagedAutoUpgradeSchedule \
    --schedule-type weekly \
    --interval-weeks 2 \
    --day-of-week Monday \
    --duration 6 \
    --utc-offset +7:00 \
    --start-time 00:00
```