# unifi-on-azure
Note: we are commiting the required files in the upcoming days. Still a work in progress for now. :-)

## Introduction
We created an ready to deploy Unifi controller for Azure. This will install the [Jacob Alberty](https://github.com/jacobalberty/unifi-docker) docker build on Azure. Almost no configuration is needed.
The Unifi controllers run's as a Container Instace in Azure and uses a Azure file share to store it's configuration data.

## Deployment
Azure provides us with multiple ways to deploy resource. Using [ARM templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/) works best for the resources we need.
#### PowerShell
We can deploy the Docker Container with PowerShell. Unfortunately due to an [issue](https://github.com/Azure/azure-cli/issues/6235) with the *--ports* and *--protocol* options it is not possible to add both the TCP and UDP ports to the container. This makes PowerShell only partially useful to deploy the container.

```PowerShell
az container create --resource-group %ResourceGroupName% --os-type Linux --name %UnitName% --image jacobalberty/unifi:stable --ip-address public --ports 3478 6789 8080 8443 8843 --protocol TCP --azure-file-volume-account-name %StarageAccountName% --azure-file-volume-account-key %Secret% --azure-file-volume-share-name %ShareName% --azure-file-volume-mount-path /unifi/ --log-analytics-workspace %LogAnalyticsWorkspaceName% --log-analytics-workspace-key %LogAnalyticsKey% --environment-variables RUNAS_UID0=false
```
#### Portal
Due to missing options in the portal it is not possible at this time to configure it manually.
The option to mount a storage account is not currently present in the wizard.

#### ARM Template
It is possible to do the deployment with an ARM template. You can find the one we use here.

#### Thing you need to do yourself
The deployment takes care of almost everything. There are still two things that need to be done by hand.
1. Add your own certificates to the fileshare in /unifi/cert.
2. Configure the controlle itself. Either by restoring from an existing back-up. Or by following the wizard. That's up to you.

### Deploy to Azure
If you like to deploy it directly to Azure, please use the link below. This wil create the storage account, docker image, an link the two together.

[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/deploybutton.png)](https://azuredeploy.net/)

## Suggestions
If you have any comments of suggestions please feel free to [add them](https://github.com/Syndicate-Consulting/unifi-on-azure/issues).

## External Links
[Jacob Alberty's Docker image for the Unifi Controller.](https://github.com/jacobalberty/unifi-docker)

[Microsoft Doc's page for the az container command.](https://docs.microsoft.com/en-us/cli/azure/container?view=azure-cli-latest)

[Microsoft Doc's page for mounting an Azure file share inside a Container Instance.](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-volume-azure-files)
