---
title: "Verificar e alterar inicialização de destino padrão para Linux"
date: 2023-07-26T11:41:14
tags: [linux]
slug: "verificar-e-alterar-inicializacao-de-destino-padrao"
---

O Systemd é responsável por gerenciar recursos de sistema do Linux. Esses recursos são conhecidos como _units_, como serviços, _targets_, _sockets_ e assim por diante. É possível usar o __systemd__ para listar todas as _units_ com o seguinte comando:

```shell
systemctl list-units
```

_Targets_ representam o estado que o Linux alcançou durante a inicialização. Também é possível executar o comando acima para filtrar apenas as _units_ do tipo _target_:

```shell
systemctl list-units type=target
```

Para obter o _target_ padrão sendo utilizado para o Linux, o seguinte comando se encaixa nesse propósito:

```shell
systemctl get-default
```

Para mudar para outro _target_, o comando `set-default` pode ajudar com esta tarefa:

```shell
sudo systemctl set-default <new-target>
```