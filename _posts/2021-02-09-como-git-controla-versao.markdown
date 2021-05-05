---
layout: single
title: "Histórico de arquivos com Git"
date: 2021-02-09 07:10:00 -0300
categories: controle-versao
tags: git cvcs dvcs histórico
---

Realizar mudanças em arquivos conforme as necessidades que surgem ao longo do tempo e possuir apenas a última versão disponível não é o suficiente em alguns casos. Alguns exemplos disso são:
{: style="text-align:justify;"}

- A versão atual não ser satisfatória e necessitar retroceder para uma versão anterior;
- Identificar quando uma mudança foi realizada e o motivo da mesma;
- Localizar a pessoa que realizou a mudança para entender melhor o contexto.
{: style="text-align:justify;"}

Para tais cenários possuir um histórico relacionado as mudanças é um caminho para ajudar resolver tais situações.
{: style="text-align:justify;"}

## Controle de versão local

Por meio de um sistema denominado RCS (_Revision Control System_ em inglês) foi possível criar e manter tal histórico.
{: style="text-align:justify;"}

Cada versão (conjunto de mudanças no arquivo) registrada no histórico do sistema representa as diferenças do conteúdo em relação a versão anterior, e essa comparação é conhecida como _patch_. Portanto, um conjunto de versões do arquivo também pode ser denominado como _patch set_.
Quando desejado restaurar uma determinada versão, baseado na versão inicial o sistema aplica todos os patches correspondentes até a versão desejada.
Podemos encontrar semelhança nesse procedimento quando é feito utilização de migrations para versionamento de banco de dados.
{: style="text-align:justify;"}

Contudo, tal histórico só ocorre localmente. Com a necessidade de ter a colaboração de outras pessoas para também realizar mudanças em tais arquivos, outras opções surgiram.
{: style="text-align:justify;"}

## Controle de versão centralizado

Um CVCS (_Centralized Version Control System_ em inglês) é uma evolução do sistema RCS.
{: style="text-align:justify;"}

Os mesmos arquivos estão disponíveis para que mais de uma pessoa possa alterá-los. Para isso, é feito o uso de um servidor. As pessoas podem, por exemplo, obter a última versão desses arquivos em suas máquinas, realizar as alterações e enviar novamente para o servidor para disponibilizar o que foi alterado para as outras pessoas. Isso permite pessoas colaborarem entre si para manter os arquivos no estado desejado além de se beneficiar das questões de histórico trazidas pelo RCS.
{: style="text-align:justify;"}

A ideia do controle de versão é semelhante ou igual ao que o sistema RCS utiliza para _patch_. Um CVCS identifica as diferenças aplicadas no arquivo com a versão anterior e registra isso como uma versão no histórico. Tal processo de comparação para identificar as diferenças é denominado _delta_ e a imagem abaixo ilustra um exemplo disso:
{: style="text-align:justify;"}

![Histórico dos arquivos baseados nos deltas]({{ site.url }}{{ site.baseurl }}/assets/images/historico-versoes-deltas.png)

Cada arquivo no sistema só possuirá uma nova versão quando for modificado.
{: style="text-align:justify;"}

O CVCS apresenta algumas desvantagens também, tais como:
{: style="text-align:justify;"}

- Único ponto de falha: como todas as operações relacionadas ao histórico dependem do servidor (checkout, visualizar histórico, commit, e etc), caso esteja ausente ou há algum problema na comunicação com ele, você ficará impossibilitado de realizar tais operações. Se, por exemplo, precisar disponibilizar suas mudanças para outras pessoas neste cenário, isso não será possível até que tal problema seja resolvido;
- Banco de dados do sistema corrompido: nesse cenário será necessário restaurar um backup. Pode haver impactos para o histórico em relação a defasagem do último backup com o que tinha no banco ou mesmo se o backup também possuir problemas. O que as pessoas possuem localmente é apenas uma versão daquilo disponível no servidor, não sendo suficiente para ajudar a contornar este problema.
{: style="text-align:justify;"}

Referência: [Git - Book](https://git-scm.com/book/en/v2)