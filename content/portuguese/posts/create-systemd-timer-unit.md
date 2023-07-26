---
title: "Criar Unit de Timer do Systemd"
date: 2023-07-26T18:30:00
tags: [linux]
slug: "criar-unit-de-timer-do-systemd"
---

Com propósito de agendar uma execução para um serviço específico em um determinado período de tempo, um arquivo _timer_ pode ajudar a atingir esse objetivo. _Timers_ são arquivos _unit_ do systemd, cujo nome é seguido pelo sufixo __.timer__, e tem essa característica. Olhando para o conteúdo do arquivo conforme demonstrado no exemplo a seguir, podemos notar a presença da seção __Timer__:

```shell
[Unit]
Description=XXXX

[Timer]
OnCalendar=*-*-* 10:30:00
Persistent=true
Unit=<service file>

[Install]
WantedBy=<target>
```

A seção __Timer__ utiliza a opção __OnCalendar__ para estabelecer quando o serviço deve ser executado (no exemplo acima, sempre às 10h30) apontando seu respectivo serviço na opção __Unit__.

Não obstante, como uma _unit_ definida por usuário, os arquivos de _timer_ e de serviço precisam estar disponíveis no diretório _/etc/systemd/system/_ para que o _target_ especificado em ambos os arquivos possa descobri-los e envolvê-los no processo de inicialização do sistema Linux.

Depois disso, a próxima etapa é executar o comando `daemon-reload` para recalcular as dependências do serviço, ativá-las para criar um link simbólico do diretório systemd do _target_ para o diretório systemd no qual elas estão disponíveis e, por último, iniciá-las. O exemplo a seguir traz a sequência desses comandos:

```shell
systemctl daemon-reload
systemctl enable <timer file> <service file>
systemctl start <timer file> service file>
```

Você pode ver o status deles usando os comandos abaixo:

```shell
systemctl status <timer file>
systemctl status <service file>
```