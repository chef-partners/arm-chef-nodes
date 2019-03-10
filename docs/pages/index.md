---
title: ARM Template for Chef Nodes in Azure
permalink: index.html
---

The templates provided here enable to creation of any number of Linux and / or Windows nodes. Once the machines have been built they will be connected up to the specified Chef server.

Where possible settings that need to be applied to both types of machine has been grouped together. However there are certain parameters that are only applicable to Windows or Linux machines.

{% include important.html content="It is assumed that the virtual network and subnet that the machines will be connected to already exists in Azure" %}

To get going immediately, click on the button below. The browser will open a page in the Azure Portal with _all_ the parameters in a form.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fchef-partners%2Farm-chef-nodes%2Fmaster%2Fsrc%2Fazuredeploy.jsonc" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

# Quickstart

For those people that are impatient and do not want to consult all of the documents to deploy into Azure the following is a quick introduction into deploying some machines into Azure.

In the example the following settings will be used, please change according to needs. This will create 1 Linux machine and 1 Windows machine. The Windows machine will have a 50Gb data disk attached to it.

Resource Group: `arm-chef-nodes-1`
Location: `westeurope`

| Parameter | Value | Description |
|----|----|----|
| prefix | `rjs` | All resources created will be prefixed with this value. This is to assist with uniqueness |
| networkRGName | `rjs-arm-1` | Resource group containing the virtual network to be connected to |
| networkSubnetName | `qsef-subnet` | Subnet within the virtual network to connect the network interface cards to |
| windowsMachineCount | 1 | Number of Windows machines to create |
| linuxMachineCount | 1 | Number of Linux macines to create |
| windowsDataDisks | `[50]` | Specify an array of integers. These will be number and size of the data disks attached |
| osAccountPassword | `Passw0rd123!` | The password to be associated with the user on the machine. The default is `azure` |
| chefServerUrl | https://mychef.example.com/rjs | Chef server URL for the nodes to reference |
| chefValidatorName | rjs-validator | Name of the validator key being used to register the machines |
| chefValidatorKey | <BASE64_STRING> | Base64 encoded string of the associated validator key |
| chefRunListWindows | role[common] | Run list to be applied to the Windows nodes |
| chefRunListLinux | role[webserver] | Run list to be applied to the Linux nodes |

Edit the `azuredeploy.parameters.json` file or create a new one based on the main template and apply the settings as required.

{% include note.html content="There are many more parameters that can be specified. Please refer to the Parameters page for more information" %}

Depending on the tool being used run the appropriate command

## AZ Command line tool

```bash
# Create a resource group
az group create -n arm-chef-node-quickstart -l westeurope

# Deploy the template into the new resource group
az group deployment create -g arm-chef-node-quickstart --parameters ./parameters.dist.json --template-uri 
```

## PowerShell

```powershell
# Create a resource group
New-AzureRMResourceGroup -Name arm-chef-node-quickstart -Location westeurope

# Deploy the template into the new resource group
New-AzureRMResourceGroupDeployment -ResourceGroupName arm-chef-node-quickstart -TemplateParameterFile .\parameters.dist.json -TemplateUri 
```

{% include image.html file="quickstart_deployment.png" alt="Quickstart Deployment" caption="Results of the Quickstart deployment into Azure" %}