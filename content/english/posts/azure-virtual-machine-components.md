---
title: "Azure Virtual Machine components"
date: 2023-03-28T06:38:54-03:00
---

In a high level what Azure virtual machine is composed of, the one's components are:

- __Resource Group__: a virtual machine is deployed into a Resource Group, that latter contains an Azure region. Deploying a virtual machine for that Resource Group means to choose in deliver a phisically virtual machine in that location in order to take closer users and/or applications will use the services hosted in it.

- __Size__: when building a virtual machine, it is necessary pick one size from a pre-configured list based on a number of CPU cores, amount of RAM and also disk performance capabilities. The choice depends on the workload scenario you have to that virtual machine. You are able to upgrade or downgrade the size has been deployed in it.

- __Network__: it represents the network activity your virtual machine will have with the rest of your environment, in which can extends to the internet activities if it should be necessary. Azure attach an internal IP address for internal communication in your Azure Virtual Network (VNet) but you are able also to allocate a public IP address for internet communication.

- __Image__: they are used to determine the operating system running in the virtual machine. An image is available from Azure Marketplace, which contains a vary pre-configured image list between basic images and those ones with applications and network settings.

- __Storage__: each virtual machine is deployed with a block device called Azure Virtual Disk (VHD). At least, one VHD is provided to host the operating system but you can apply additional virtual disks. Those VHDs depends on the data workload you have in mind for size and disk performance capabilities.