---
title: "SSH Tunnel for Network Traffics"
date: 2023-08-02T07:15:26
tags: [linux]
---

SSH tunnel is Port forwarding via SSH in which you will able to pass traffic that it can use an unencrypted protocol over an encrypted network stream. The command is:

```shell
ssh -f <remote address> -L <local port>:<remote address>:<remote port>
```