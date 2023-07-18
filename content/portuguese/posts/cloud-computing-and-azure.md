---
title: "Computação em Nuvem e Azure"
date: 2023-07-18T18:57:23
tags: [azure]
slug: "computacao-em-nuvem-e-azure"
---

Computação em Nuvem significa usar recursos de computação de outra pessoa e em outro lugar em data centers remotos em todo o mundo. Existem algumas características em torno deste tema, como:

- __Tolerância a falhas__: A abordagem para replicar a solução em mais de um local, a fim de reduzir o tempo de inatividade para consumir esses serviços quando você enfrentar qualquer falha. É como "backup", aplicado para aplicativos, dados e assim por diante.

- __Alta Disponibilidade__: A finalidade de aproximar os usuários dos serviços que eles irão consumir. No que diz respeito à localização do dispositivo, tem-se a disponibilidade de consumir os mesmos serviços em uma região mais próxima ao invés da de origem com o objetivo de reduzir o tempo.

- __Escalabilidade__: É o processo de aumentar a capacidade de computação para atender às necessidades do seu negócio.

- __Elasticidade__: É o processo inverso para escalabilidade, ou seja, diminuir a capacidade computacional para corresponder às necessidades que você tem naquele momento.

## Regiões e Zonas de Disponibilidade do Azure

A região do Azure é uma coleção de data centers individuais criados nesse local. Dentro de uma região, pode haver outra divisão conhecida como Zonas de Disponibilidade.

As Zonas de Disponibilidade são compostas por um ou vários edifícios físicos de data centers. Cada uma das zonas é independente de energia, rede e assim por diante. A finalidade das zonas de disponibilidade na mesma região é adicionar uma camada extra para _tolerância a falhas_ oferecendo a capacidade de replicar os serviços em várias zonas.

Em um cenário em que os serviços são implantados em várias regiões, você obtém _tolerância a falhas_ e _alta disponibilidade_, pois além de poder replicar a implantação para minimizar o tempo de inatividade, você consegue aproximar os usuários para consumir esses serviços. Essa abordagem protege contra a interrupção da região.

Em um cenário em que a implantação usa uma região com zonas de disponibilidade, você obtém apenas _tolerância a falhas_. Ele protegerá contra ponto único de falha.

## Gerenciador de Recursos do Azure (ARM)

Independentemente da abordagem para criar e manipular os recursos do Azure (portal do Azure, Azure Powershell, CLI do Azure ou clientes REST), todos aqueles que executarem tais comandos irão interagir com uma camada centralizada conhecida como Gerenciador de Recursos do Azure (ARM). Ele também centraliza a autenticação.