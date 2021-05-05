---
layout: single
title: Objetos armazenados pelo Git
date: 2021-05-04 08:00:00 -0300
categories: controle-versao
tags: git objeto blob tree commit tag
---

Ao inicializar um repositório Git, uma estrutura de arquivos e diretórios é criada correspondente ao exemplo abaixo:
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-git-estrutura-inicial.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-git-estrutura-inicial.JPG" alt="Estrutura de um repositório Git inicializado">
    </a>
</figure>

Podemos observar que no caminho _.git/objects/_ é o local onde diferentes tipos de objeto que compõe o histórico do repositório são armazenados. Ao inicializá-lo, não consta nenhum objeto:
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-diretorio-vazio.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-diretorio-vazio.JPG" alt="Diretório de objetos vazio">
    </a>
</figure>

## Objeto Blob

Quando um arquivo é enviado para a Staging Area, o Git efetua um snapshot referente ao seu conteúdo para amazená-lo como um objeto do tipo **blob**. Esse conteúdo será utilizado para definir seu checksum, qual será utilizado como nome do objeto no repositório.
{: style="text-align:justify;"}

Como exemplo, ao adicionarmos na Staging Area um arquivo README com o conteúdo _Instruções para setup do projeto_, o diretório **objects** possuirá o seguinte item:
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-criado-objeto-blob-no-repositorio.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-criado-objeto-blob-no-repositorio.JPG" alt="Criação de um objeto blob">
    </a>
</figure>

Caso outro arquivo seja criado com o mesmo conteúdo, o Git não criará mais um objeto do tipo blob porque tal conteúdo já possui seu respectivo checksum. Podemos observar no exemplo abaixo que após adição de outro arquivo com mesmo conteúdo, como encontra-se a Staging Area:
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-adicionado-outro-arquivo-mesmo-conteudo.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-adicionado-outro-arquivo-mesmo-conteudo.JPG" alt="Adicionado outro arquivo com mesmo conteúdo na Staging Area">
    </a>
</figure>

## Objeto Tree

O diretório raiz e todo subdiretório será armazenado no Git como objeto **tree**. No momento em que é executado um commit, o Git realizará um snapshot do diretório para obter a lista de arquivos e diretórios correspondentes. O checksum de um objeto tree é baseado nos respectivos nomes dos itens dessa lista. Essa informação passa a ser utilizada no nome do objeto.
{: style="text-align:justify;"}

Será vinculado para cada item da lista a referência do seu respectivo checksum, isto é, qual é o seu respectivo conteúdo no momento que o commit foi realizado. Abaixo consta um exemplo do que podemos encontrar ao visualizar o conteúdo de um objeto tree. Nele consta dois arquivos e um subdiretório, este último qual possui também um arquivo:
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-conteudo-objeto-tree.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-conteudo-objeto-tree.JPG" alt="Conteúdo de 2 objetos tree">
    </a>
</figure>

Pelo tipo na lista (blob ou tree) podemos identificar se o nome refere-se para um arquivo ou subdiretório.
{: style="text-align:justify;"}

**OBS**: _Dessa forma, há a possibilidade de comparar as mudanças ocorridas naquele diretório ao longo do tempo. O mesmo racícionio pode ser atribuído para os objetos blob_. 
{: style="text-align:justify;"}

**OBS2**: _Diretórios vazios são desconsiderados pelo Git, portanto, não haverá objetos tree correspondentes_.
{: style="text-align:justify;"}

## Objeto Commit

Ao realizar um commit, juntamente com o objeto tree, um objeto **commit** é criado. Algumas informações deste objeto é comumente vistas na utilização do comando `git log`. No conteúdo deste objeto, podemos visualizar dados como o nome e e-mail do autor, data e mensagem do commit, além de uma referência para um objeto tree. Este objeto tree sempre corresponde ao diretório raiz do repositório.
{: style="text-align:justify;"}

Dessa forma, quando utilizado, por exemplo, comandos tais como `git checkout`, `git reset` ou `git revert`, no qual explicitamente ou implicitamente (pode mencionar a branch, por exemplo) é apontado qual commit (objeto commit) deve ser analisado, através dessa referência ao objeto tree - snapshot aplicado no momento do commit - e as referências subsequentes nos objetos posteriores que o Git é capaz de restaurar o conteúdo dos arquivos e diretórios para a data e hora do commit.
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-dados-objeto-commit.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/objetos-dados-objeto-commit.JPG" alt="Conteúdo de um objeto commit">
    </a>
</figure>

## Objeto Tag

Este objeto é criado quando uma tag annotated é atribuída para um commit. [Aqui]({{ site.url }}{{ site.baseurl }}/controle-versao/utilizacao-tags-not-git/) possui mais informações sobre isso.
{: style="text-align:justify;"}

Referências: 
- [Git - Book](https://git-scm.com/book/en/v2)
- [Git - git-cat-file Documentation](https://git-scm.com/docs/git-cat-file)
- [Git Book - The Git Index](https://shafiul.github.io//gitbook/7_the_git_index.html)