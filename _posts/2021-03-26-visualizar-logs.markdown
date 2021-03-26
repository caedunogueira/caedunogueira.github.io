---
layout: single
title: "Visualizar logs no Git"
date: 2021-03-26 08:00:00 -0300"
categories: controle-versao
tags: git log terminal
---

Há diversas maneiras de visualizar o histórico de um repositório Git, tanto por ferramentas gráficas quanto pelo terminal.
{: style="text-align:justify;"}

Pelo terminal isso é possível através do comando `git log`, que fornece diversas opções.
{: style="text-align:justify;"}

Ao utilizar o comando com a opção `git log -p` é possível visualizar nos commits quais foram as mudanças ocorridas entre aquele commit e seu antecessor.
{: style="text-align:justify;"}

Já com o uso das opções `git log --name-only` e `git log --name-status` serão exibidos os nomes dos arquivos que receberam uma nova versão no commit. O comando `git log` não permite que tais opções sejam utilizadas juntas (_a opção `--name-status` já contempla o resultado da opção `--name-only`_).
{: style="text-align:justify;"}

## Formatação

O comando `git log` possui uma formatação padrão para exibição dos dados do commit porém essa formatação é passível de mudança. Podem ser utilizados formatos pré-estabelecidos ou customizar seu próprio formato. Para o uso desses formatos, existe a opção `--pretty`. Dentre os pré-estabelecidos, temos:
{: style="text-align:justify;"}
- `git log --pretty=oneline`, qual pela sintaxe `git log --oneline` fornece o mesmo resultado
- `git log --pretty=short`
- `git log --pretty=full`
- `git log --pretty=fuller`
{: style="text-align:justify;"}

Para utilizar seu próprio formato pode ser feito uso da opção `git log --pretty="format:<formatação>"`, como no exemplo abaixo:
{: style="text-align:justify;"}

```bash
git log --pretty="format:%h %d - %s - (%an | %ad)"
```

A formatação permite informar dados do commit no qual o comando realizará interpolação de strings para exibição na tela. O git fornece diversos campos como dados do commit, dentre alguns deles:
{: style="text-align:justify;"}
- **%H**, hash do commit
- **%h**, hash do commit abreviado
- **%d**, indica se a HEAD ou alguma branch possui ponteiro indicado para aquele commit
- **%s**, mensagem do commit
- **%an**, nome do autor do commit
- **%ad**, data absoluta que o autor criou o commit
- **%ar**, data relativa que o autor criou o commit
- **%cn**, nome do committer
- **%cd**, data absoluta que o committer, por exemplo, aprovou um PR que possuia o commit
- **%cr**, data relativa que o committer, por exemplo, aprovou um PR que possuia o commit
{: style="text-align:justify;"}

Também é possível adicionar estilos para o formato como uma forma de apresentar um destaque para as informações. Para configurar estilo para um campo, use a sintaxe _%C([estilo a ser aplicado])_ antes do campo em si. Veja o exemplo abaixo:
{: style="text-align:justify;"}

```bash
git log --pretty="format:%C(red bold)%h%Creset %C(cyan)%d%Creset %s (%C(yellow)%an%Creset - %C(green italic)%ad%Creset)"
```

<figure>
    <a href="{{ site.url}}{{ site.base.url}}/assets/images/exemplo-formatacao-com-git-log.JPG" class="align-center">
        <img src="{{ site.url}}{{ site.base.url}}/assets/images/exemplo-formatacao-com-git-log.JPG" alt="Resultado do comando acima exemplificado">
    </a>
</figure>

É possível observar o uso de **%Creset** na formatação. O **%Creset** impede que o estilo informado antes dele seja propagado para o restante do texto.
{: style="text-align:justify;"}

## Filtro

Em algumas situações o resultado do comando `git log` pode ser correspondente a um filtro. Em um repositório com histórico relativamente grande, isto facilita visualizar/localizar a informação desejada. A opção `git log -<quantidade de commits>` restringe a visualização dos últimos commits no repositório para a quantidade informada. A opção `-<quantidade de commits>` é uma sintaxe para `-n <quantidade de commits>`.
{: style="text-align:justify;"}

É possível também aplicar um filtro pelo autor do commit, com a opção `git log --author=<nome>`.
{: style="text-align:justify;"}

Já a opção `git log --grep=<texto a ser pesquisado>`  ajuda a exibir somente commits nos quais contém na sua mensagem o texto a ser pesquisado.
{: style="text-align:justify;"}

Se o propósito é filtrar por um determinado conteúdo em um ou mais arquivos, a opção `git log -S <texto a ser pesquisa>` pode ser útil nessa questão. Contudo, vale ressaltar que a opção `-S` baseará sua pesquisa somente em conteúdo que foi introduzido/removido nos arquivos que acarretou em uma nova versão deles nos commits. Em outras palavras, a opção `git log -S` aplicará um filtro no resultado correspondente a opção `git log -p`.
{: style="text-align:justify;"}

Algumas vezes pode ser interessante avaliar commits que foram introduzidos em determinado período. As opções `git log --since` e `git log --until` auxiliam nesse tipo de filtro, nas quais podem ser utilizadas tanto isoladas quanto combinadas.
{: style="text-align:justify;"}

Referências:
- [Git - Book](https://git-scm.com/book/en/v2)
- [Git - git-config Documentation](https://git-scm.com/docs/git-config)
- [Git - pretty-formats Documentation](https://git-scm.com/docs/pretty-formats)
- [A better git log (Example)](https://coderwall.com/p/euwpig/a-better-git-log)