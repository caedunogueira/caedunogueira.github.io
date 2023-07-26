---
title: "Journal Control to investigate service logs"
date: 2023-07-26T18:50:00
tags: [linux]
---

When you face with a problem in one of the service and would like to investigate about its execution through logs, you can use the __Journal Control__ to this task as mentioned in the below command:

```shell
journalctl -u <service file>
```

Service is an example but the option -u can be used to any unit file, either system or user-defined one.