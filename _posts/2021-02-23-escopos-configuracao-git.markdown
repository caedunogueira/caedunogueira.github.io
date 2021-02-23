---
layout: single
title: "Escopos de configuração no Git"
date: 2021-02-23 08:03:00 -0300
categories: controle-versao
tags: sistema global local git
---

As variáveis de configuração de um repositório estão atreladas para um escopo. O escopo permite que a variável seja compartilhada com outros repositórios. Dentre os possíveis escopos, temos:
{: style="text-align:justify;"}

- **Sistema**: neste escopo, uma variável será compartilhada entre repositórios de todos os usuários daquela máquina. Para definir uma variável neste escopo utilize a opção `--system`.
- **Global**: também com o propósito de compartilhar a variável entre repositórios porém restringe-se por usuário da máquina. Para definir uma variável neste escopo utilize a opção `--global`.
- **Local**: neste caso a variável limita-se a ser aplicada apenas para o repositório em si. Este é o escopo padrão.
{: style="text-align:justify;"}

Ainda que uma variável seja definida em mais de um escopo, a precedência utilizada pelo Git começa do mais restritivo até o menos restritivo, isto é, na direção do Local para o Sistema.
{: style="text-align:justify;"}

Com o comando `git config --list` é possível exibir todas as configurações utilizadas para aquele repositório.
{: style="text-align:justify;"}

A opção `--list` pode ser combinada com a opção `--show-origin` para exibir qual o arquivo (e sua localização) está definido aquela variável. Também pode ser combinado com a opção `--show-scope` para exibir o escopo daquela variável.
{: style="text-align:justify;"}

Referência: [Git - Book](https://git-scm.com/book/en/v2)