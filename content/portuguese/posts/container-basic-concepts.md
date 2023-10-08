---
title: "Conceitos Básicos Contêineres"
date: 2023-10-08T12:08:41-03:00
tags: [container]
slug: "conceitos-basicos-conteineres"
---

## Máquinas Virtuais e Contêineres

Uma abordagem para a implantação de software como uma solução portátil é usar máquinas virtuais. As máquinas virtuais são capazes de emular o sistema operacional adequado necessário para esse aplicativo, sendo executadas sobre o sistema operacional do host nesse bare metal. No entanto, isso considera um alto uso dos recursos do host que alavancam os custos. Outro ponto a ser trazido para a discussão como outro exemplo é o dimensionamento dos aplicativos. Não é simples nem rápido fornecer outra instância de aplicativo devido ao tempo de inicialização de uma nova máquina virtual, ou seja, o tempo para rodar outra réplica desse sistema operacional junto com os componentes necessários. Por um lado, é possível provisionar uma máquina virtual que executa um sistema operacional, independentemente do sistema operacional do host. Por outro lado, é difícil lidar com os custos e a escalabilidade.

A outra abordagem para a implantação de software como soluções portáteis é usar Contêineres. A pequena diferença em relação às máquinas virtuais é que o ambiente isolado usará os recursos do kernel diretamente do sistema operacional do host. Ao fazer isso, os contêineres são considerados menores, mais baratos e mais rápidos do que as máquinas virtuais, porque você pode ativar mais instâncias no mesmo host (devido ao consumo de menos recursos do que as máquinas virtuais) e essas instâncias são fornecidas em termos de segundos em vez de minutos. Por um lado, você tem as vantagens mencionadas na última frase; por outro lado, é menos portátil do que as máquinas virtuais. Por exemplo, é possível ter contêineres Linux executados sobre o sistema operacional host como Windows, mas o oposto não é possível, ou seja, contêineres Windows executados sobre o sistema operacional host usando Linux.

## Orquestração

Atualmente, softwares complexos no ambiente de produção precisam usar escalabilidade e elasticidade para lidar com todo o tráfego de forma adequada, aproveitando as melhores opções de uso de recursos (custos) e desempenho. Para atingir esse objetivo, uma maneira é usar uma ferramenta de orquestração como o Kubernetes. Essas ferramentas nos ajudam com muitas atividades que eram feitas manualmente no passado, como a implantação de tempo de inatividade ou instâncias de aplicativos que apresentavam problemas durante a execução.

### Implantação sem tempo de inatividade

Em um cenário para atualizar a versão do aplicativo em um ambiente de produção, você enfrenta o desafio de minimizar o impacto que o processo de atualização pode ter sobre ele, escolhendo a melhor abordagem para reduzir ao máximo o tempo que o servidor levaria para aplicar essas alterações. Um exemplo para ilustrar isso é aplicar as alterações ao ambiente em um período de tempo que tenha o menor consumo para o aplicativo. Às vezes, o processo pode proporcionar uma situação imprevista, como problemas com uma nova versão, para a qual é necessário dar um passo atrás, adotar um plano de reversão para a versão atual e fazer uma avaliação para entender o que aconteceu.

Uma ferramenta de orquestração contém uma abordagem para superar esse problema, considerando a implantação do processo sem tempo de inatividade. Como uma tarefa automatizada, com base nas métricas coletadas, é possível ativar novos contêineres com a versão mais recente do aplicativo e manter os contêineres antigos com a versão atual. Durante todo o processo, a ferramenta transferirá o tráfego, pouco a pouco ou em um ritmo escolhido pela pessoa responsável, dos contêineres antigos para os novos. Os contêineres antigos serão removidos somente se, de acordo com as métricas apresentadas, não houver problemas com a nova versão do aplicativo nos novos contêineres. Os contêineres mais novos tomarão o lugar dos antigos. Tudo isso sem interferência humana no processo.

### Autocorreção de aplicações

Com base nas métricas, quando uma ferramenta de orquestração identifica um contêiner com problemas, é fácil para ela substituir automaticamente o contêiner problemático por um saudável. Todas essas etapas são realizadas automaticamente pela ferramenta, proporcionando mais resiliência ao aplicativo. A substituição leva alguns segundos. Essa abordagem em que a ferramenta toma esse tipo de decisão (com base em algumas configurações estabelecidas por alguém, é claro) sem interferência humana é chamada de autocorreção, ou seja, o processo em que o aplicativo se "conserta" no ambiente.

## História

Na década de 1970, os computadores mainframe eram um recurso escasso para as empresas devido ao seu custo. Isso levou ao desenvolvimento de computadores centralizados e ao compartilhamento de recursos entre vários usuários.

Em 1979, o primeiro passo para uma solução de conteinerização foi usar o comando chroot. O comando chroot altera a raiz. Ele altera o diretório aparentemente raiz de um processo e de todos os seus processos filhos. Isso significa que o processo e todos os processos filhos gerados a partir dele estão limitados à visualização da estrutura de arquivos somente a partir desse ambiente chroot.

Na década de 1990, Bill Cheswick queria criar um ambiente que lhe permitisse estudar as teclas digitadas pelos crackers para rastreá-los e aprender suas técnicas. Sua solução foi usar um ambiente chrooted e começar a fazer modificações. O resultado seria o que conhecemos hoje como o comando jail do Linux.

Em 4 de março de 2000, o FreeBSD introduziu o comando jail do FreeBSD em seu sistema operacional. Embora fosse semelhante ao comando chroot, ele também incluía recursos adicionais de sandboxing de processos para isolar o sistema de arquivos, os usuários, a rede etc. Ele fornecia mais controle sobre esses ambientes isolados.

Em 2006, os engenheiros do Google anunciaram contêineres de processos projetados para isolar e limitar o uso de recursos de um processo. Em 2007, esses contêineres de processos foram renomeados como Control groups (Cgroups) para evitar confusão com a palavra contêiner. Posteriormente, eles foram adotados no kernel do Linux e permitiram o desenvolvimento de algumas tecnologias, como o LXC. LXC significa Linux Containers (Contêineres Linux) e fornece virtualização no nível do sistema operacional, permitindo que vários ambientes Linux isolados (contêineres) sejam executados em um kernel Linux compartilhado.

Havia outros grupos de pessoas estudando abordagens melhores para gerenciar seus clusters. Em 2009, o Mesos começou como um projeto de pesquisa no laboratório RAD da UC Berkeley e foi apresentado pela primeira vez como Nexus. O nome Nexus entrou em conflito com outro projeto universitário e foi alterado para Mesos.

Em 2013, com o uso do LMCTFY, os aplicativos puderam ser escritos para serem sensíveis a contêineres e, portanto, programados para criar e gerenciar seus próprios subcontêineres. O Docker foi lançado como um projeto de código aberto em 2013. O Docker ajudou a fornecer a capacidade de empacotar contêineres para que eles pudessem ser movidos de um ambiente para outro. O Docker Swarm v1.0 foi lançado em 3 de novembro de 2015. O Swarm permite que os aplicativos do Docker sejam executados em escala em um cluster. O Kubernetes é um sistema de orquestração de contêineres de código aberto que foi fortemente influenciado pelo sistema Borg do Google. Foi anunciado em meados de 2014, com o Kubernetes v1.0 sendo lançado em 21 de julho de 2015.

O Docker Swarm fornece gerenciamento de cluster e funcionalidade de orquestração, permitindo que os contêineres sejam executados em um cluster de máquinas.

Para evitar qualquer confusão com o uso do termo contêineres, os contêineres de processo foram renomeados como __Control groups__ ou __Cgroups__.