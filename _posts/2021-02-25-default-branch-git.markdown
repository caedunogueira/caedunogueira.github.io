---
layout: single
title: "Definir nome da branch default no Git"
date: 2021-02-25 06:54:00 -0300
categories: controle-versao
tags: branch git
---

Ao utilizar o comando `git init`, por default, o Git cria uma branch com nome default **master**. Contudo, é possível modificar esse nome na criação dos próximos repositórios por meio da configuração _init.defaultBranch_. Abaixo segue um exemplo em como realizar essa alteração no escopo global:
{: style="text-align:justify;"}

```bash
git config --global init.defaultBranch [nome desejado]
```

Referência: [Git - Book](https://git-scm.com/book/en/v2)