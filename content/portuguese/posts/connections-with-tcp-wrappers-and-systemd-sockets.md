---
title: "Conexões com TCP Wrappers e Sockets do Systemd"
date: 2023-08-02T07:30:13
tags: [linux]
slug: "conexoes-com-tcp-wrappers-e-sockets-do-systemd"
---

Você pode criar uma camada extra para conexões usando Sockets do Systemd com TCP Wrappers. Em primeiro lugar, precisamos verificar se o `sshd.socket` está parado:

```shell
systemctl status sshd.socket
```

Caso contrário, podemos usar o comando abaixo para atingir esse objetivo.

```shell
systemctl stop sshd.socket
```

A próxima etapa pode ser criar um _job_ para interromper `sshd.service` e iniciar `sshd.socket`. Os seguintes comandos auxiliam nesta tarefa:

```shell
sudo at now + 3 minutes
at > systemctl stop sshd.service
at > systemctl start sshd.socket
```

O comando `Ctrl + D` permitirá finalizar a edição e agendar o _job_ para o horário proposto. Depois que o socket do Systemd foi iniciado, você pode verificar a presença da biblioteca TCP Wrapper:

```shell
ldd /usr/sbin/sshd | grep libwrap
```

A última etapa é permitir e negar conexões para o host para permitir apenas conexões de _socket_ sshd. Abra o arquivo `/etc/hosts.allow` para anexar a linha `sshd2 sshd : ALL`. O próximo arquivo a ser alterado é `/etc/hosts.deny` com a instrução `ALL : ALL`.