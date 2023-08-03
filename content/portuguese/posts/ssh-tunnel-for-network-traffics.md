---
title: "Tunel SSH para Tráfego de Rede"
date: 2023-08-02T07:15:26
tags: [linux]
slug: "tunel-ssh-para-trafego-de-rede"
---

O túnel SSH é o encaminhamento de porta via SSH no qual você poderá passar o tráfego que pode usar um protocolo não criptografado em um fluxo de rede criptografado. O comando é:

```shell
ssh -f <remote address> -L <local port>:<remote address>:<remote port> -N
```