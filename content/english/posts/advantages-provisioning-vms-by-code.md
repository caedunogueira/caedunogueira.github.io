---
title: "Advantages provisioning virtual machines by code"
date: 2023-04-03T06:45:06-03:00
tags: [azure]
---

Some of the advantages using code to provisioning virtual machines are:

- _consistency_: you are able to create virtual machines with the same characteristics regardless the amount required to that deploy. Besides that, you can follow the changes for this resource using system version control.

- _automation_: due to the steps are the same to deploy that resource, they are candidates to automate them, helping to repeat themselves every time as needed. It avoids make some mistakes whereas could appear when apply those steps manually.

- _replication_: build down-level environments, such as dev/test ones based on the production environment, helping the test cycles. Building similar environments help replicate the production configuration easily.