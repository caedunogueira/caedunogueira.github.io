---
title: "Kubernetes - Parte 1"
date: 2024-02-11T10:30:00-03:00
tags: [kubernetes]
slug: "kubernetes-parte-1"
---

O Kubernetes é um orquestrador de contêineres criado para ser executado usando uma arquitetura de contêineres, ou seja, um cluster que contém um nó mestre (o nó _control plane_) e nós escravos (os nós de trabalho). Um nó _control plane_ é responsável apenas por gerenciar os nós de trabalho e garantir sua integridade para executar suas cargas de trabalho. O nó _control plane_ não terá nenhuma carga de trabalho em execução para se tornar um nó mais robusto e eficiente, o que aumenta as chances de evitar que um problema ocorra nele devido a um problema de carga de trabalho.
O nó _control plane_ exporá sua API, o que permite gerenciar e interagir com o cluster.

Por outro lado, o nó de trabalho será responsável pela execução de todas as cargas de trabalho nesse cluster. Cargas de trabalho significam toda a estrutura/objetos que fazem parte do Kubernetes, além dos contêineres de aplicativos. Os nós de trabalho são máquinas virtuais alocadas como nós para fazer parte do cluster. A diferença entre a virtualização em uma máquina virtual e a virtualização em um contêiner é que a virtualização em uma máquina virtual ocorre no nível do hardware, enquanto a virtualização em um contêiner ocorre no nível do sistema operacional.

O contêiner é um processo do sistema operacional que usa recursos do sistema e faz _syscalls_ para o kernel gerenciado pelo _container engine_. O _cotainer engine_ é responsável por aplicar limites a esse processo em termos de uso de recursos e permitir que as _syscalls_ sejam enviadas ao kernel. Esse processo (contêiner) e seus filhos são isolados do restante do sistema operacional como uma abordagem conhecida como namespace.

Cada contêiner representa uma imagem em execução. Uma imagem de contêiner é uma definição de um ambiente em um formato de leitura.

O estado do nó de trabalho representa um conjunto de dados referentes às cargas de trabalho em execução nesse nó, como o número de cargas de trabalho, as variáveis de ambiente passadas a ele, o nome, a versão e assim por diante.

Para gerenciar o cluster, a API no nó _control plane_ precisa de muitas informações dos nós de trabalho. Mas, ao mesmo tempo, o objetivo da API é ser simples o suficiente, e isso não é possível em termos de complexidade, em que cada nó tem uma maneira de extrair alguns dados ou executar alguns comandos, por exemplo. Para manter em mente uma API simples, outro componente entra em cena para ajudar no gerenciamento do cluster. Ele é chamado de __kubelet__.

O Kubelet é um componente para nós de trabalho que recebe comandos da API para serem executados e para obter os dados necessários para que o _control plane_ avalie o estado do nó, saiba mais sobre suas cargas de trabalho e assim por diante.

## Pod

O pod é o menor recurso publicável no nó de trabalho. O pod é uma abstração do processo em execução em um cluster e é capaz de conter um conjunto de contêineres.
Embora um pod possa representar um conjunto de contêineres, na maioria das vezes é mais um cenário de exceção do que uma regra, porque se você tiver alguns aplicativos em execução no mesmo pod e houver um problema com ele, todos esses aplicativos ficarão indisponíveis.

Há um cenário em que alguém pode ser motivado a agrupar contêineres em um pod, como se um componente não existisse sem o outro, como um forte acoplamento. Exceto isso, a ideia (ou o que será visto) será um contêiner por pod.

Todos os processos executados em um pod compartilharão os mesmos recursos, como CPU, memória, volume, rede e assim por diante, semelhante a uma máquina virtual. Ao mesmo tempo, todos os processos podem se comunicar uns com os outros via localhost, pois estão na mesma rede. Fora do pod, todos eles terão o mesmo endereço IP, mas uma porta diferente. Portanto, se você tiver um contêiner na porta X, não terá outro contêiner usando a mesma porta.

Os pods são __efêmeros__. Isso significa que eles não devem ser considerados persistentes.

### Recursos

Pensando nos nós de trabalho como máquinas com recursos escassos, o arquivo de manifesto do Pod tem uma chave chamada __resources__ que permite definir o uso mínimo e máximo de CPU e memória para esse contêiner. O estabelecimento dessas configurações é considerado uma boa prática devido à escassez de recursos disponíveis nos nós.

A chave __resources__ tem duas outras chaves chamadas __requests__ e __limits__. Cada uma delas pode usar as chaves, a __cpu__ e a __memory__ para fornecer os recursos necessários, sejam os máximos ou os mínimos a serem usados.

Para a chave __cpu__, o valor 1 representa 100% do uso da CPU. É o mesmo que 1000m (milicores).
Para a chave de __memory__, o valor está em bytes, seguido de uma das unidades disponíveis (E, P, G, M e K).

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod-name
spec:
  containers:
    - name: my-container-name
      image: my-container-image
      resources:
        requests:
          cpu: 100m
          memory: 150M
        limits:
          cpu: 400m
          memory: 550M
      ports:
        - containerPort: 8080
```

Quando o nó _control plane_ recebe uma ordem para criar um novo pod, isso não significa que o pod será criado ao mesmo tempo, porque o processo que o nó _control plane_ realizará é agendar esse evento, pois é necessário avaliar se há um nó capaz de alocar esse pod em relação aos limites de recursos estabelecidos para ele. Você não receberá um erro com o comando create, mas lembre-se de que, às vezes, ele não ocorrerá ao mesmo tempo.

O nó _control plane_ obterá a CPU e a memória restantes disponíveis no nó (diferença entre CPU e memória disponíveis e CPU e memória alocadas para todas as cargas de trabalho em todos os namespaces) e as comparará com os limites de recursos estabelecidos para o novo pod. A API seguirá as próximas etapas somente se houver um nó capaz de alocá-lo. Por outro lado, ela mantém o estado do pod pendente.
Usar o comando `kubectl describe pod <pod-name>` ajuda a ver a lista de eventos que ocorreram nesse pod, incluindo aqueles entre a etapa de agendamento e a criação de um.

### Finzalização normal

O pod é considerado efêmero. Outras cargas de trabalho que não têm um volume anexado a elas têm a mesma característica. Quando você aplica o comando `kubectl delete pod <pod-name>`, a API aguarda um período, o padrão é 30 segundos, para que o pod encerre sua execução. Se esse tempo não for respeitado, a API enviará um sinal SIGNKILL para forçar o encerramento de sua execução. O período de espera pode ser alterado pela flag `--grace-period`. Para excluir o pod sem esperar esse tempo, a flag `-f` pode ser usada.

```shell
kubectl delete pod <pod-name> --grace-period=<number>
```

```shell
kubectl delete pod <pod-name> -f
```