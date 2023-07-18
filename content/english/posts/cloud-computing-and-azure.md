---
title: "Cloud Computing and Azure"
date: 2023-07-18T18:57:23
tags: [azure]
---

Cloud Computing means use compute resources from someone else and somewhere else in remote data centers around the world. There are some characteristics around this subject, such as:

- __Fault Tolerance__: The approach for replicate the solution more than one place in order to reduce downtime to consume those services when you face with any crash. It is like "backup", applied for applications, data and so on and sor forth.

- __High Availability__: The purpose to take closer users that services they will consume for. Regard to device location, it has available to consume the same services in a nearer region instead of origin one with the goal to reduce the time.

- __Scalability__: It is the process to increase the compute capacity to match the needs for your business.

- __Elasticity__: It is the reverse process for scalability, that is, to shrinks the compute capacity to match the needs you have for that moment.

## Azure Regions and Availability Zones

Azure Region is a collection of individual data centers built in that single location. Inside a region, there can be another division knwon as Avalability Zones.

Availability Zones are composed by one or multiple physical data centers buildings. Each of them are independent from power, networking and so on. The purpose of availability zones in the same region is to add an extra layer for _fault tolerance_ by offering the ability to replicate the services across multiple zones.

In a scenario in which the services are deployed into multiple regions, you get both _fault tolerance_ and _high availability_, because besides you are able to replicate the deploy to minimize the downtime your are able to take closer users to consume those services. That approach defend against region outage.

In a scenario that deploy uses one region with availability zones, you get only _fault tolerance_. It will protect against single point of failure.

## Azure Resource Manager (ARM)

Regardless the approach to create and handle Azure resources (Azure portal, Azure Powershell, Azure CLI or REST Clients), all of those to execute these commands will interact with a centralized layer known as Azure Resource Manager (ARM). It also centralizes authentication.