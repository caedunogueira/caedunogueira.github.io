---
layout: single
title: "Os estágios de um arquivo no Git"
date: 2021-02-15 09:00:00 -0300
categories: controle-versao
tags: modified staged committed repositório git
---

Ao utilizar um repositório Git local, há um fluxo em relação as mudanças que um arquivo seguirá conforme os estágios abaixo:

- _Modified_
- _Staged_
- _Committed_

## Modified

No repositório, há um espaço no qual é registrado as modificações nos arquivos e estrutura de diretórios sob uma determinada versão (hash) escolhida pelo usuário. Este espaço é conhecido como _Working Tree_. Ao utilizar no terminal o comando `git status` em que é visualizado (não tenho certeza se tais configurações de cores podem ser modificadas) arquivos e diretórios em vermelho, esta cor remete ao conteúdo da Working Tree.

A Working Tree é o primeiro estágio quando se trata de gerar um novo estado para aquele repositório. As modificações podem refletir um ou vários motivos, qual podem ser discriminados nos estágios seguintes.

Caso deseja desfazer uma mudança detectada na Working Tree, isso também é possível. Assim, o arquivo e/ou diretório estará novamente conforme a versão do hash.

## Staged

O próximo estágio é indicar para o Git quais mudanças pertencerão ao próximo estado, isto é, corresponderão a nova versão. A seleção se dará baseada nas mudanças detectadas pela Working Tree. No terminal o comando `git add` permite selecionar algumas ou todas as mudanças detectadas lá.

Quando tais mudanças são adicionadas, elas são registradas em um arquivo dentro do repositório .git. Neste momento, elas encontram-se na _Staging Area_ (alguns chamam por _index_). Com o comando `git status` é possível identificar dentre as mudanças que estavam na Working Tree quais foram selecionadas para estar na Staging Area, qual remete a cor verde.

Se várias mudanças foram realizadas na Working Tree mas deseja-se que elas sejam discriminadas no histórico (qual conterá informações do autor, mensagem do hash/estado/versão, data e hora e etc) então pode ser adicionado as desejadas, seguir para o próximo estágio, e depois retornar novamente para Staging Area para adicionar novas mudanças. Como comentado, é possível fazer isso de uma vez ou aos poucos, conforme a necessidade.

A partir desse ponto, é possível tanto retirar as mudanças selecionadas e devolvê-las para a Working Tree quanto avançar para o último estágio.

## Committed

Nesta etapa será registrado no histórico as mudanças adicionadas na Staging Area. Ao utilizar o comando `git commit` um snapshot de todo o repositório é realizado, conforme comentado [aqui]({{ site.url }}{{ site.baseurl }}/controle-versao/como-git-controla-versao-parte-2/index.html). Um snapshot também é comumente denominado de _commit_. Com o comando `git log` é possível visualizar todos os commits realizados, o que corresponde a visualização do histórico deste repositório.

Um commit também pode ser revertido, isto é, pode-se retornar a uma determinada versão dos arquivos baseado em outro commit do histórico.

Referência: [Git - Book](https://git-scm.com/book/en/v2)