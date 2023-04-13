---
title: "Authentication using Azure CLI"
date: 2023-04-03T07:01:45-03:00
tags: [azure]
---

There are two ways in order to authenticate in Azure using Azure CLI:

- Interactive mode
- Service Principal mode

## Interactive mode

```sh
az login
```

It allows you authenticate in Azure launching the Azure's authentication page in a browser to manually provide the username and password.

## Service Principal mode

```sh
az login --service-principal
```

It is ideal for scenarios used by automated tools. You will need to create one (if it does not exist yet) by either `az ad sp create` command or `az ad sp create-for-rbac` command, last giving the according permissions for the Azure resources.
Instead of granting full access to those tools it is recommended use service principal with restrictive permissions.
The parameter `--service-principal` must be provided with others to authenticate in that mode.