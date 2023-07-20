---
title: "Azure Resources Hierarchy"
date: 2023-07-20T12:19:55
tags: [azure]
---

There is a resources organization in Azure applied at 5 levels, such as:

- Tenant
    - Management Group
        - Subscriptions
            - Resource Group
                - Resources

One of the advantages of that organization is a centralize manner to set up permissions. Permissions applied in one level will be replicated to the lower levels. For example, access policy established for a set of identities and roles to a specific subscription means all resources belong to it will conform with those policies. For maintenance of that policy, modify in one place will replicate changes to all resources available in that subscription.
The centralized authorization can be applied for all levels.

## Tenant

Tenant is a single instance that represents the organization, like Microsoft, McDonalds, Warner Bros and so on. The tenant is top level of hierarchy and it contains all users directory or identities directory the company will give specific permission for some Azure resources.

## Management Group

The purpose of Management Group is centralize multiple subscriptions into one place. It is not required use Management Group but one advantage, besides to arrange subscriptions, is the benefit to use the centralized authorization in which you are able apply the same access policy for some subscriptions at the same time.

## Subscriptions

Subscription is a component that represents payment agreement has choosen to pay the use for Azure resources. Each subscription has its own billing agreement.

## Resource Group

As a good practice, to keep together all resources either belonging to the same project or belong to the same life cycle, Resource Group is a way to do that.

## Resources

They are virtual machines, storages services, networking, and so on.