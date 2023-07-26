---
title: "Check and change the default target boot for Linux"
date: 2023-07-26T11:41:14
tags: [linux]
---

To check the default target boot has been used in Linux, the following command can be used:

```shell
systemctl get-default
```

And to change for different default target, it could be used:

```shell
sudo systemctl set-default <new-default-target>
```