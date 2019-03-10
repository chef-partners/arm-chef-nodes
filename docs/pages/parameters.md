---
title: Parameters
permalink: parameters.html
---

There are a number of parameters that can be set on these templates. The following table details them all.

{% include note.html content="If a parameter does not have a dfeayult value then it will be considered compulsory bu the Azure tooling" %}

| Name | Description | Type | Default Value | Example Value |
|---|---|---|---|---|
| prefix | All resources will be prefixed with this value. This is to assist with the uniqueness of names of resources | string | | `rjs` |
| networkRGName | Name of the resource group containing the network to connect to | string | | `rjs-arm-1` |
| networkVnetName | Name of the existing virtual network | string | | `qsef-vnet` |
| networkSubnetName | NAme of the existing subnet | string | | `qsef-subnet` |
| windowsMachineCount | How many Windows machines to create. It is possible to set zero here. | integer | `1` | 
| linuxMachineCount | How many Linux machines to create. It is possible to set zero here. | integer | `1` | 
| windowsOS | Which version of Windows to create the machine with | string | `2016-Datacenter` | |
| linuxOS | Which version of Ubuntu to create the Linux machines with | string | `18.04-LTS` | |
| windowsVMSize | The size of VM to use when creating the Windows machines | string | `Standard_DS2_V2` | |
| linuxVMSize | The size of VM to use when creatung the Linux machines | string | `Standard_DS2_V2` | |
| linuxDataDisks | The number and size of data disks to create. (See Notes) | string | [] | |
| windowsDataDisks | The number and size of data disks to create. (See Notes) | string | [] | |
| osAccountName | Name of the account to create on the machine | string | `azure` | |
| osAccountPassword | Password to be set on the account that is created | string | | `Password123!` |
| osAccountSSHKeys | Array of public SSH keys to be applied to Linux machines | string[] | | ["ssh-public-key-string] |
| chefServerUrl | The URL to the Chef server that the nodes should be registered with | string | | `https://mychef.example.com/rjs` |
| chefValidatorName | Name of the validator to use when registering the machine | string | | `rjs-validator` |
| chefValidatorKey | Base64 encoded string of the validator key for the specified validator | string | | `lkjlkjlkjljljk` |
| chefRunListLinux | RUn list to applied to Linux machines | string | | `role[moveiedb]` |
| chefRunListWindows | Run list to be applied to Windows machines | string | | `role[webserver]` | 
| chefNodeSSLVerifyMode | Whether the client should verify the SSL certs from the Chef server or not. This is useful for self-signed certificates | `peer` | `none` |
| chefEnvironment | The environment that the node(s) should be added to on the Chef server | `_default` | `staging` |
| chefClientConfiguration | Any extra client configuration that should be passed roto the client that cannot be set using the extension parameters. | string | | | 
| chefClientVersion | The version of the Chef client to install on the nodes | string | `14.11.21` | |
| enableBootDiagnostics | Whether or not to enable boot diagnostics. See notes. | boolean | `false` | `true` |
| location | The location in which to create the resources | string | Same as the RG being deployed into | `eastus` |
| uniqueShort | What the unqiue short character should be. If not specified it will be randmonly generated | string | | | 

## Notes

### Data disks

When creating data disks for the machines an array with the sizes of the disks, in Gb,  must be specified. For example for the Windows machines to have 2 data disks, one of 100Gb and one of 150Gb the JSON would be as follows:

```json
{
  "windowsDataDisks": {
    "value": [100, 150]
  }
}
```

### Enable Boot Diagnostics

A storage account will only be created if `enableBootDiagnostics` is set to `true`. a Storage account is not required for the general running of a machine as disks are now resources in their own right.
