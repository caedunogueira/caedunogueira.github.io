---
title: "Check and change the default target boot for Linux"
date: 2023-07-26T11:41:14
tags: [linux]
---

Systemd is responsible to manage Linux system resources. Those resources are known as units, such as services, targets, sockets and so on. It is possible to use systemd to list all of units are made of by the following command:

```shell
systemctl list-units
```

Targets represent the state of Linux has reached during startup. It is also possible to run the above command to filter only for target units:

```shell
systemctl list-units --type=target
```

To get the default target boot has been used for Linux, the following command fit the purpose:

```shell
systemctl get-default
```

To change to another target, the `set-default` command can help with this task:

```shell
sudo systemctl set-default <new-target>
```