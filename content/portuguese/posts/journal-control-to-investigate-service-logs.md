---
title: "Journal Control para investigar logs de serviço"
date: 2023-07-26T18:50:00
tags: [linux]
slug: "journal-control-para-investigar-logs-de-servico"
---

Quando você se depara com um problema em um dos serviços e deseja investigar sobre sua execução através de logs, pode utilizar o __Journal Control__ para esta tarefa conforme mencionado no comando abaixo:

```shell
journalctl -u <service file>
```

O serviço é um exemplo, mas a opção -u pode ser usada para qualquer arquivo _unit_, seja do sistema ou definido pelo usuário.