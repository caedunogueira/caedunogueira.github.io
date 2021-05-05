---
layout: single
title: "Utilização de tags no Git"
date: 2021-04-09 08:05:00 -0300
categories: controle-versao
tags: git tag
---

No histórico do repositório, como mais um adendo - se preferir - para como organizá-lo/construí-lo, é possível estabelecer marcos, isto é, pontos no histórico que possam  facilitar a identificação do que se possui até aquele momento. Por exemplo, uma das maneiras em que esses marcos são estabelecidos é atribuir uma versão para aquele ponto. A informação da versão pode conter as principais mudanças registradas até ali.
{: style="text-align:justify;"}

No Git é possível estabelecer esses marcos por meio de **tags** com uso do comando `git tag`. Uma **tag** é um rótulo a ser definido para um commit.
{: style="text-align:justify;"}

Há 2 tipos de tags que podem ser utilizados no repositório: _Lightweights_ e _Annotateds_.
{: style="text-align:justify;"}

## Lightweight
{: style="text-align:justify;"}

Nessa abordagem o Git registra uma referência do hash do commit (objeto commit) para a tag. Isso equivale a um arquivo em _.git/refs/tags_, no qual o nome do arquivo corresponde ao rótulo atribuído para a tag.
{: style="text-align:justify;"}

Para fazer uso desse tipo, nenhuma outra opção do comando `git tag` deve ser utilizada:
{: style="text-align:justify;"}

```bash
git tag <rótulo> [hash commit]
```

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/referência-commit-para-tag.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/referência-commit-para-tag.JPG" alt="Referência do commit para tag ao utilizar tipo lightweight">
    </a>
</figure>

## Annotated

Nessa abordagem, o Git armazena um objeto a mais em seu banco do tipo tag com as informações sobre o rótulo. As informações vinculadas neste objeto são:
{: style="text-align:justify;"}
- Hash do objeto atrelado a tag
- Tipo do objeto atrelado a tag
- Rótulo
- Tagueador (autor da tag)
- Mensagem da tag
{: style="text-align:justify;"}

A referência em _.git/refs/tags_ passa a ser para o hash deste objeto do tipo tag ao invés do hash do objeto commit. A opção `git tag -a` denota o tipo annotated porém uma vez omitido, com o uso da opção `git log -m` o Git implicitamente entende que a tag corresponde a este tipo.
{: style="text-align:justify;"}

```bash
git tag -a -m <mensagem> <rótulo> [hash commit]
```

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/referência-object-para-tag.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/referência-object-para-tag.JPG" alt="Referência do objeto para tag ao utilizar tipo annotated">
    </a>
</figure>

Portanto, enquanto no tipo _lightweight_ o Git fará referência na tag para um objeto já existente (porque o objeto do commit exisitirá independente da tag existir) no tipo _annotated_ será acrescentado um objeto a mais no banco que servirá para acrescentar informações adicionais desejadas e vinculá-lo para o rótulo.
{: style="text-align:justify;"}

## Atualização no repositório remoto

Para atualizar o repositório remoto com as tags adicionadas, pode ser feito uso do comando push para levar todas as tags:
{: style="text-align:justify;"}

```bash
git push origin --tags
```

ou pode utilizá-lo para uma tag específica:
{: style="text-align:justify;"}

```bash
git push origin [rótulo da tag]
```

## Exclusão

Quanto a exclusão, no repositório local pode ser feito uso do comando:
{: style="text-align:justify;"}

```bash
git tag -d <rótulo>
```

E dentre os caminhos para excluir remotamente, há o comando:
{: style="text-align:justify;"}

```bash
git push origin --delete <rótulo>
```

Referência: [Git - Book](https://git-scm.com/book/en/v2)