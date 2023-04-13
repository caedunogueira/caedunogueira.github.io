---
title: "Componentes de uma Máquina Virtual do Azure"
date: 2023-03-28T06:38:54-03:00
tags: [azure]
slug: "components-maquina-virtual-azure"
---

Em um alto nível sobre a composição de uma máquina virtual do Azure, seus componentes são:

- __Resource Group__: uma máquina virtual é implantada baseado em um Resource Group, esse último qual contém uma região do Azure. Implantar uma máquina virtual para aquele Resource Group significa escolher disponibilizar uma máquina virtual fisicamente naquele local com o propósito de trazer mais próximo usuários e/ou aplicações daquela região que irão utilizar os serviços hospedados nela.

- __Tamanho__: ao construir uma máquina virtual, é necessário pegar um _tamanho_ de uma lista pré-configurada baseado no número de núcleos do CPU, quantidade de RAM e também nas capacidades de performance do disco. A escolha depende do cenário de carga de trabalho que você tem para aquela máquina virtual. Você é capaz de modificar o tamanho para um tamanho mais sofisticado ou mais simples em relação ao já existente.

- __Rede__: representa a atividade de rede da sua máquina virtual que irá ter com o resto do seu ambiente, na qual pode estender para atividades de internet se for necessário. O Azure anexa um endereço IP interno para comunicação interna com a sua Azure Virtual Network (VNet) mas você é capaz também de alocar um endereço IP público para comunicação com a internet.

- __Imagem__: elas são usadas para determinar o sistema operacional em execução na máquina virtual. Uma imagem está disponível no Azure Marketplace, qual contém uma lista variada de imagens pré-configurada entre imagens básicas e imagens com configurações de aplicações e rede.

- __Armazenamento__: cada máquina virtual é implantada com um dispositivo chamado Azure Virtual Disk (VHD). Pelo menos, um VHD é fornecido para hospedar o sistema operacional mas, você pode acrescentar outros discos virtuais. Esses VHDs depende da carga de trabalho de dados que você tem em mente para o tamanho e capacidade de performance do disco.