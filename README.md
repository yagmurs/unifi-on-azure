# unifi-on-azure
## Introduction
This 

### PowerShell
We can deploy the Docker Container with PowerShell. Unfortunately due to an [issue](https://github.com/Azure/azure-cli/issues/6235) with the --ports and --protocol options it is not possible to ad both the TCP and UDP ports to the container. This makes PowerShell only partially usefull to deploy the container.

''''PowerShell
az container create --resource-group %ResourceGroupName% --os-type Linux --name %UnitName% --image jacobalberty/unifi:stable --ip-address public --ports 3478 6789 8080 8443 8843 --protocol TCP --azure-file-volume-account-name %StarageAccountName% --azure-file-volume-account-key %Secret% --azure-file-volume-share-name %ShareName% --azure-file-volume-mount-path /unifi/ --log-analytics-workspace %LogAnalyticsWorkspaceName% --log-analytics-workspace-key %LogAnalyticsKey% --environment-variables RUNAS_UID0=false
''''

## Deploy to Azure
If you like to deploy it directly to Azure, please use the link below. This wil create the storage account, docker image, an link the two together.

[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/deploybutton.png)](https://azuredeploy.net/)

## Suggestions
IF you have anny comments of suggestions please feel free to [add them](../unifi-on-azure/issues).

## External Links
Jacob Alberty's Docker image for the Unifi Controller.  This is the image we use for the container.
https://github.com/jacobalberty/unifi-docker

Microsoft Doc's page for the az container command.
https://docs.microsoft.com/en-us/cli/azure/container?view=azure-cli-latest

Microsoft Doc's page for mounting an Azure file share inside a Container Instance.
https://docs.microsoft.com/en-us/azure/container-instances/container-instances-volume-azure-files
