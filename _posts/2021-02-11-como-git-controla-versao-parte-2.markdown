---
layout: single
title: "Histórico de arquivos com Git - parte 2"
date: 2021-02-11 07:50:00 -0300
categories: controle-versao
tags: git dvcs histórico
---

Em continuidade ao que foi comentado na primeira parte, para contornar as desvantagens apresentadas em um CVCS, sistemas (Git, Mercurial) com característica DVCS surgiram.
{: style="text-align:justify;"}

## Controle de versão descentralizado

Diferente do CVCS, um DVCS (_Distributed Version Control System_ em inglês) disponibilizará não somente uma versão do histórico que se encontra no servidor/repositório central mas sim **todo** o seu histórico. Neste sistema o histórico é *distribuído* para todos que desejam colaborar com as mudanças nos arquivos, não mais fica centralizado em um único ponto.
{: style="text-align:justify;"}

Dessa forma, a maior parte das operações para lidar com esse histórico não necessitam comunicar-se com o servidor, são executadas localmente, já que há uma cópia do repositório na máquina. Isso torna tais operações rápidas de serem executadas já que não há mais dependência de comunicação de rede e possíveis problemas de latência.
{: style="text-align:justify;"}

Quanto ao problema de banco de dados corrompido (lembre-se, ainda há um repositório que servirá para as pessoas disponibilizarem suas mudanças para outras pessoas e sincronizarem seus trabalhos), com esse modelo distribuído, várias máquinas podem servir como backup para restaurar o repo central.
{: style="text-align:justify;"}

### Histórico no Git

Ao invés de gerar versões delta para os arquivos, sempre que ocorre uma mudança em um dos arquivos o Git gera uma nova versão no histórico para todos os arquivos. Ele realiza um snapshot do estado atual daqueles arquivos e isso resulta em uma nova versão para todos, como pode ser visto no exemplo da imagem abaixo:
{: style="text-align:justify;"}

![Histórico dos arquivos no Git]({{ site.url }}{{ site.baseurl }}/assets/images/historico-versoes-git.png)

De fato, nem sempre ocorre mudanças em todos os arquivos. Para os arquivos que não foram modificados, o Git faz uma referência (como se fosse algo como link simbólico do Linux) para a versão anterior, então você não tem aquele conteúdo duplicado para cada versão, o que implica também no tamanho desse histórico no repositório do Git.
{: style="text-align:justify;"}

Cada versão corresponde a um estado desse repositório, e toda vez que há um estado novo, um hash é atribuído a ele. É utilizado SHA-1 para criação desse hash e tem como base a estrutura de diretórios e o conteúdo dos arquivos naquele estado. Quando utilizado no terminal o comando `git log`, cada hash corresponde a um snapshot comentado acima e o hash em si diz respeito ao conteúdo deste snapshot.
{: style="text-align:justify;"}

 _Obs: claro, há mais informações que podem ser visualizadas com o comando `git log`_
{: style="text-align:justify;"}

Referência: [Git - Book](https://git-scm.com/book/en/v2)