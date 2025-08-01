# Update Configuration Command
## Config Auto Update
```bash
az aks update \
    --resource-group $RG \
    --name $AKS \
    --auto-upgrade-chanel stable \
    --node-os-upgrade-chanel securitypatch
```

## Set Maintenance Configuration
### Set update Node OS schedule 
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

### Set update cluster schedule
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