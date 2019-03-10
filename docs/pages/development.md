---
title: Development
permalink: development.html
---

When developing or just deploying from a local workstation there are some handy tools that have been added to the repo. These are Typescript scripts that need to be transpiled into Node scripts.

These tools copy the templates into a working directory and then (optionally) upload them to a container in Azure Blob storage.

Once the files are in a public location the tools can then deploy the templates from there. The tools will create and destroy the resource groups as required.

## Requirements

In order to use these tools the following is required:

 - A valid Azure Service Principal Name (SPN) saved in `${HOME}/.azure/credentials`
 - Azure Blob storage with public access (optional)
 - Node and NPM installed

## Building the tools

The libraries that the tools depend on need to be installed and then the tools generated, for example:

```bash
# Install the necessary libraries
npm install

# Build the tools
npm run compile:scripts
```

## Configuration

In order to upload the files to the Azure Blob storage, a configuration file is required. By default the tools will look for a file called deploy.json.

{% include note.html content="This file is not in source control because it is unique to each situation" %}

This file is a JSON file and accepts the following settings.

| Setting | Description | Example |
|---|---|---|
| `resourceGroup.name` | Name of the resource group to create. This will be suffixed by the iteration number | `rjs-arm` |
| `dirs.working` | Where the template files should be copied to on local disk before upload | `build/working` |
| `storageAccount.name` | Name of the storage account for files to be uploaded to | `kjh76566asdalkj` |
| `storageAccount.container` | Container in the Storage account to put the files into | `templates` |
| `storageAcount.groupName` | Resource group that has the storage account as one of its resources | `rjs-storage` |

When a deployment is run a `.deploy` file will created. This is a JSON file that contains the name of the resource group and the iteration that was last used. This is how the tools keep track of what resource group has been created.

## Using the tools

After compiling the tools and setting up the configuration it can be used to deploy the templates.

### Copy the files into the working directory

```bash
node bin/build.js copy
```

### Upload the files to the Storage Account

The Azure subscription ID has to be specified on the command line. This is the subscription that the Storage Account resides in and where the deployment will occur.

```bash
node bin/deploy.js upload [SUBSCRIPTION_ID]
```

### Deploy the templates from the Storage Account

Again the subscription has to be specified. In addition the parameters file to use needs to be specified.

```bash
node bin/deploy.js deploy [SUBSCRIPTION_ID] --parameters src/azuredeploy.parameters.json
```
