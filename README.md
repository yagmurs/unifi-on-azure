# unifi-on-azure

## Introduction
We created an ready to deploy Unifi controller for Azure. This will install the [Jacob Alberty](https://github.com/jacobalberty/unifi-docker) docker build on Azure. Almost no configuration is needed.
The Unifi controllers run's as a Container Instance in Azure and uses a Azure file share to store it's configuration data.

## Deployment
Azure provides us with multiple ways to deploy resource. Using [ARM templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/) works best for the resources we need.

#### Thing you need to do yourself
The deployment takes care of almost everything. There are still two things that need to be done by hand.
1. Add your own certificates to the file share in /unifi/cert.
2. Configure the controller itself. Either by restoring from an existing back-up. Or by following the wizard. That's up to you.

#### Accessing the controller
After the deployment is complete you can locate the containers IP.

![alt text](https://raw.githubusercontent.com/Syndicate-Consulting/unifi-on-azure/master/Unifi%20Docker%20IP.jpg?raw=true)

Browse to the web interface by navigating to __https:// *ip* :8443__

![alt text](https://github.com/Syndicate-Consulting/unifi-on-azure/blob/master/Unifi%20Docker%20Web.jpg?raw=true)

### Deploy to Azure
If you like to deploy it directly to Azure, please use the link below. This will create the storage account, docker image, an link the two together.

[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/deploybutton.png)](https://azuredeploy.net/)

## Suggestions
If you have any comments of suggestions please feel free to [add them](https://github.com/Syndicate-Consulting/unifi-on-azure/issues).

## External Links
[Jacob Alberty's Docker image for the Unifi Controller.](https://github.com/jacobalberty/unifi-docker)

[Microsoft Doc's page for the az container command.](https://docs.microsoft.com/en-us/cli/azure/container?view=azure-cli-latest)

[Microsoft Doc's page for mounting an Azure file share inside a Container Instance.](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-volume-azure-files)
