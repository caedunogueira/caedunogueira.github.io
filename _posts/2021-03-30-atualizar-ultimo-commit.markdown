---
layout: single
title: "Atualizar último commit no Git"
date: 2021-03-30 07:40:00 -0300"
categories: controle-versao
tags: git commit
---

Após registrar um commit, é possível que lembre de uma ou mais mudanças que precisavam ser feitas. Nem sempre as próximas mudanças - como neste caso - correspondem ao desejo do usuário de realizar mais um snapshot pois faria sentido que também estivessem no último commit.
{: style="text-align:justify;"}

Um dos caminhos seria adicionar tal commit e aplicar um squash para torná-los um só. Contudo, uma outra abordagem é "atualizar" o último commit com as novas mudanças.
{: style="text-align:justify;"}

Isso é possível com a opção `--amend` que consta no comando `git commit`:
{: style="text-align:justify;"}

```bash
git commit --amend
```

Ao aplicá-la, é possível constatar que o commit foi "atualizado" com as mudanças adicionadas na Staging Area pelo uso do comando:
{: style="text-align:justify;"}

```bash
git log -p -1
```

No fim, o que o Git faz para "atualizar" o último commit é **descartá-lo** da sua branch e adicionar um novo, no qual o antecessor do commit descartado passa a ser antecessor deste novo commit. É possível observar isso pela mudança de hashs no último commit antes e depois dessa operação.
{: style="text-align:justify;"}

O commit descartado ainda existe, tanto é que você pode apontar o ponteiro do HEAD para ele com o comando `git checkout` se ainda possuir o hash - ou hash abreviado - em mãos. Você estará _detached_ (desanexada) com sua branch.
{: style="text-align:justify;"}

Com isso, é possível evitar aqueles commits adicionais (que pode trazer uma impressão de poluição para o histórico) por conta de ter esquecido de uma ou outra mudança que desejava ter adicionado ao último commit.
{: style="text-align:justify;"}

**Obs**: Deve-se atentar ao utilizar esta opção caso já tenha atualizado seu repositório remoto com o commit descartado. Neste cenário, para aplicar uma nova atualização no remoto, o Git solicitará primeiro que você realize uma atualização local - `git pull` - e isso acarretará em um merge commit, qual talvez não seja o resultado esperado no histórico pelo usuário.
{: style="text-align:justify;"}

Referência: [Git - Book](https://git-scm.com/book/en/v2)