---
layout: single
title: Branchs no Git
date: 2021-05-06 08:10:00 -0300
categories: controle-versao
tags: git branch
---

Uma branch é uma abordagem em seguir com o desenvolvimento/alteração de algo apartado da _linha principal_/_linha de referência_ de trabalho no seu repositório, está última que, pode ser definida como aquela que conterá apenas mudanças já concluídas e estáveis.
{: style="text-align:justify;"}

Dessa forma, é possível isolar de outros desenvolvimentos que continuam sendo sincronizados na linha principal por demais pessoas as mudanças em andamento e/ou instabilidades que possam ocorrer enquanto é realizado tal trabalho.
{: style="text-align:justify;"}

Há VCSs (_Version Control Systems_ em inglês) que para disponibilizar a existência de uma branch realiza uma cópia/duplicação de arquivos e diretórios da branch de referência. Com o passar do tempo e com a criação de mais branchs, isso pode acarretar em um aumento significativo do tamanho do seu repositório.
{: style="text-align:justify;"}

Contudo, o Git lida de maneira diferente com a criação de branchs. Nele, uma branch é apenas um ponteiro móvel para o conjunto de commits existente no repositório. Ele possui um arquivo qual o nome refere-se ao nome da branch, onde seu conteúdo mantém o hash do commit para qual a branch se encontra. Isso tudo equivale a 41 bytes (40 bytes do hash adicionado ao caractere de nova linha), o tamanho de uma branch no Git.
{: style="text-align:justify;"}

A branch mudou de commit? Somente é atualizado o conteúdo desse arquivo com o hash do commit correspondente. Criou uma nova branch? São 41 bytes adicionais. Excluir branch no Git também é um processo simples, isto é, o que ele precisa se ater é na exclusão de tal arquivo e não em excluir cópias/duplicidades de arquivos e diretórios que estariam atreladas a ela.
{: style="text-align:justify;"}

Abaixo podemos visualizar em _.git/refs/heads_ o arquivo correspondente a branch _main_ e em seu conteúdo o hash no qual encontra-se atualmente a branch (exibido no comando `git log`):
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/branchs-exemplo-main.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/branchs-exemplo-main.JPG" alt="Exemplo de ponteiro da branch main para o commit">
    </a>
</figure>

Neste outro exemplo é demonstrado a utilização de 2 branchs, como permanece o diretório _.git/refs/heads_ e o conteúdo de seus arquivos:
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/branchs-exemplo-com-duas.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/branchs-exemplo-com-duas.JPG" alt="Exemplo com utilização de 2 branchs">
    </a>
</figure>

## HEAD

O HEAD é um ponteiro que indicará localmente ou em qual branch você se encontra ou em qual commit (este último se você estiver no modo _DETACHED_). Ele armazena essa informação no arquivo _HEAD_ localizado em _.git/_. Abaixo podemos notar a mudança no conteúdo deste arquivo com a utilização do comando `git checkout`:
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/branchs-exemplo-HEAD.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/branchs-exemplo-HEAD.JPG" alt="Exemplo de alternância no conteúdo do arquivo HEAD com o comando git checkout">
    </a>
</figure>

![Imagem ilustrativa de outro repositório com utilização de branchs]({{ site.url }}{{ site.baseurl }}/assets/images/branchs-imagem-livro-git.png)

Referência: [Git - Book](https://git-scm.com/book/en/v2)