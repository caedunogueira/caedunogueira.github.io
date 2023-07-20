---
title: "Azure IAM Components"
date: 2023-07-20T18:49:21
tags: [azure]
---

There are 3 components used for Azure Identity Authorization Management:

- Azure Active Directory
- Azure Role-Based Control
- Scopes

## Azure Active Directory

It belongs to top of resources hierarchy, in which identify and prove you are who you are saying you are. Once the identity has been resolved, the role and permissions can set to that identity. Each identity in Azure in known as security principal because identity can represents users, applications and so on.

## Azure Role-Based Control (Azure RBAC)

It provides fine-grained access management to Azure resources.
Roles is a collection of individual permissions. Individual permissions, for instance, such creating virtual machines, viewing virtual machines and other similar examples like that. A bundle of specific permissions is assigned to a role.
The role is assigned to security principal.

## Scopes

Scopes is a set of resources to grant access and it has directly relation to resource hierarchy.