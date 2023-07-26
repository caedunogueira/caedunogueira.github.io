---
title: "Verificar e alterar inicialização de destino padrão para Linux"
date: 2023-07-26T11:41:14
tags: [linux]
slug: "verificar-e-alterar-inicializacao-de-destino-padrao"
---

Para verificar a inicialização de destino padrão usada no Linuz, o seguinte comando pode ser utilizado:

```shell
systemctl get-default
```

E para mudar para um diferente destino padrão, pode ser usado:

```shell
sudo systemctl set-default <new-default-target>
```