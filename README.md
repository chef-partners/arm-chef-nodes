# ARM Templates for Chef Nodes

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fchef-partners%2Farm-chef-nodes%2Fmaster%2Fsrc%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

This repo contains the ARM templates necessary to create and configure machines in Azure that are Chef nodes. This supports both Windows and Linux machines.

Currently it is assumed that the Virtual Network and Subnet that the machines need to connect to already exists.

## Quickstart

Ensure that the `az` tool or PowerShell is logged into the Azure subscription being deployed to and has the correct permissions.

Update or take a copy of the `azuredeploy.parameters.json` file and edit for the environment being created.

Run the following command, depending on the tool being used, to deploy the template into Azure.

NOTE: In both examples a generic Resource Group is created, this may need to be modified to prevent clashes with other groups.

### AZ tool

```bash
# Create a resource group
az group create -n arm-chef-node-quickstart -l westeurope

# Deploy the template into the new resource group
az group deployment create -g arm-chef-node-quickstart --parameters ./parameters.dist.json --template-uri https://raw.githubusercontent.com/chef-partners/arm-chef-nodes/master/src/azuredeploy.json
```

### PowerShell

```powershell
# Create a resource group
New-AzureRMResourceGroup -Name arm-chef-node-quickstart -Location westeurope

# Deploy the template into the new resource group
New-AzureRMResourceGroupDeployment -ResourceGroupName arm-chef-node-quickstart -TemplateParameterFile .\parameters.dist.json -TemplateUri "https://raw.githubusercontent.com/chef-partners/arm-chef-nodes/master/src/azuredeploy.json"
```

## Documentation

For more detailed documentation please refer to the [ARM Templates for Chef Nodes](https://chef-partners.github.io/arm-chef-nodes) documentation website.

If you find a mistake or an error in the documentation then please raise an issue here so we can fix it or submit the correction using a PR.

Is it possible to run the documentation locally, if you have cloned this repo and have Docker installed. To do so run the following:

## Linux / MacOS

```bash
docker run --rm -it --volume "docs/:/srv/jekyll" -p 4000:4000 jekyll/jekyll:3.8 jekyll serve
```

## PowerShell

```powershell
docker run --rm -it --volume "${PWD}/docs/:/srv/jekyll" -p 4000:4000 jekyll/jekyll:3.8 jekyll serve
```

{% include image.html file="quickstart_deployment.png" alt="Quickstart Deployment" caption="Results of the Quickstart deployment" %}