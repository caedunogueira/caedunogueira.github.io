---
layout: single
title: "Arquivos rastreados e não rastreados no Git"
date: 2021-03-03 06:40:00 -0300
categories: controle-versao
tags: git
---

Dentro do seu diretório de trabalho, o Git identifica arquivos e/ou diretórios de 2 maneiras:
{: style="text-align:justify;"}

- Itens rastreados (_tracked_)
- Itens não rastreados (_untracked_)
{: style="text-align:justify;"}

_Itens rastreados_ são todos aqueles que encontram-se em algum commit no seu repositório em relação ao commit indicado no ponteiro do HEAD, isto é, o commit atual e todos os anteriores. Uma vez rastreado, poderá ser interpretado entre os estágios como:
{: style="text-align:justify;"}

- Unmodified
- Modified
- Staged
- Committed
{: style="text-align:justify;"}

O contrário, isto é, itens não contidos em nenhum dos commits são identificados como _não rastreados_. Ao utilizar o comando `git status` estes também serão destacados na cor vermelha sob algum título como **Untracked files**. Assim como um item rastreado e modificado, para que um item **não** rastreado pertença ao próximo commit, deve ser feito uso do comando `git add`.
{: style="text-align:justify;"}

A forma comumente no qual é entendido o comando `git add` é **adicionar itens que pertencerão ao próximo snapshot/commit**.
{: style="text-align:justify;"}

## Adição para Staging Area

A opção `--all` do comando `git commit` só é aplicada para itens rastreados quais foram alterados ou deletados. Tal opção não se aplica para itens não rastreados. Suponha que há 2 arquivos no repositório conforme imagem abaixo:
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/exemplo-rastreamento-1.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/exemplo-rastreamento-1.JPG" alt="Arquivos adicionados para o repositório">
    </a>
</figure>

Então adicionamos mais um arquivo no diretório de trabalho. Ao ser adicionado, será identificado como um item _não rastreado_.
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/exemplo-rastreamento-2.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/exemplo-rastreamento-2.JPG" alt="Mais um arquivo adicionado para o repositório como não rastreado">
    </a>
</figure>

Ao utilizar o comando `git commit -a -m "Adicionado terceiro arquivo"` podemos observar que nada foi adicionado para a Staging Area. Como resultado do próprio comando, há uma indicação que neste cenário (de itens não rastreados) deve ser feito uso do comando `git add`.
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/exemplo-rastreamento-3.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/exemplo-rastreamento-3.JPG" alt="Nada foi adicionado na Staging Area">
    </a>
</figure>

## Itens não rastreados em relação ao HEAD

A partir do HEAD, o Git analisará os respectivos commits para indicar se um item é ou não rastreável. Como um commit é um snapshot dos arquivos adicionados na Staging Area em um dado momento, a mudança na posição do HEAD - de um commit para o outro - poderá indicar itens que antes eram rastreáveis como não rastreáveis. Suponha que temos um repositório com os commits abaixo:
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/commits-repositorio-exemplo.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/commits-repositorio-exemplo.JPG" alt="Commits de um repositório">
    </a>
</figure>

Se checarmos o diretório de trabalho, o **file3** será exibido na lista de arquivos. Podemos modificá-lo e na sequência utilizar o comando `git status` para confirmar que o Git identificou que antes _unmodified_ agora o arquivo encontra-se _modified_.
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/arquivo-modificado-repositorio.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/arquivo-modificado-repositorio.JPG" alt="Modificado arquivo rastreado">
    </a>
</figure>

Vamos alterar a posição do HEAD para o commit anterior (apenas para efeitos de exemplo, seguiremos DETACHED mas também aplicá-se quando alterna entre branchs):
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/mudanca-posicao-HEAD.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/mudanca-posicao-HEAD.JPG" alt="Mudança na posição do HEAD">
    </a>
</figure>

Se optarmos por listar novamente o conteúdo do nosso diretório de trabalho, notaremos que agora o **file3** não consta. Se aplicado o mesmo comando assim quando o HEAD acompanhava o commit da branch main - adição de um contéudo para o arquivo - significará para o Git que um _novo arquivo e não rastreável_ foi adicionado ao diretório de trabalho.
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/adicionado-arquivo-nao-rastreado.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/adicionado-arquivo-nao-rastreado.JPG" alt="Adicionado arquivo não rastreado">
    </a>
</figure>

Se adicionarmos um commit a partir desse ponto, podemos observar que há **file3** em mais de um commit, neste caso, adicionados em momentos diferentes.
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/commit-mesmo-arquivo-para-outro-ramo.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/commit-mesmo-arquivo-para-outro-ramo.JPG" alt="Resultado dos commits para arquivos não rastreados">
    </a>
</figure>

Referência: [Git - Book](https://git-scm.com/book/en/v2)