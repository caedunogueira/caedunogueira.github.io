---
title: "Draft - Domain-Driven Design"
date: "2026-09-02T13:51:00-03:00"
tags: [domain-driven-design, ddd]
draft: true
---

Segundo o autor, quanto mais raso o seu conhecimento no domínio, maiores as chances de modelagem fracassarem. O autor incentiva o profissional a mergulhar no domínio em que irá trabalhar o máximo que puder, inclusive com adoção da prática de estudar materiais sobre o tema antes de conversar com os especialistas, utilizando esses últimos para validar o conhecimento adquirido.

Pela Taxonomia de Bloom, o nível mínimo de profundidade no conhecimento do domínio deveria ser de Compreender (explicar). É dito que nesse processo, o aprofundamento corresponde para uma investigação:
- qual motivo dessa funcionalidade. Por que ofertá-la como serviço/produto?
- quais características dessa funcionalidade/demanda?
- quais as partes envolvidas?
- o que cada um ganha e perde?

Ainda que no mesmo time tenha pessoas com papéis diferentes em relação ao domínio e a tecnologia, o autor compreende que a chave para desenvolver com sucesso uma demanda de negócio (transformar a demanda em uma implementação) passa pelo nível de coesão envolvido na solução da demanda.

A coesão, nesse contexto, corresponde para a proximidade entre a demanda de negócio e a solução tecnológica, isto é, quão mais próximo esses pontos estão um do outro, maior será sua coesão. Coesão, assim por dizer, o entendimento do negócio e como é tangibilizado por meio da tecnologia.
Quanto maior esse distanciamento entre esses pontos pela pessoa desenvolvedora, maior é o risco do projeto.

Dando sequência, o autor faz comentários em relação a linguagem ubíqua. A linguagem ubíqua é entendida pelos termos utilizados no dia a dia pelos envolvidos no projeto. E, essa comunicação deve refletir no código e vice-versa.
O desafio da linguagem ubíqua está na sua manutenção. É entendido como fácil criar um documento inicial com os termos em comum utilizados pelos membros do projeto. O complicado é evoluir/manter esse documento atualizado conforme as mudanças acontecem no projeto ao longo do tempo.
Idealmente, a linguagem ubíqua deve refletir as expressões/termos utilizados no idioma mencionado, ainda que ocorra uma mistura de idiomas utilizados para esses termos. Quando opta-se por uma tradução de idioma, é preciso que todas as palavras sejam traduzidas da mesma forma para todos mas, abre uma brecha para interpretações diferentes.

Além disso, os termos não devem condizer somente ao negócio. Se há uso de termos técnicos em comum por todos, estes também devem fazer parte da linguagem ubíqua.

Bounded Context (Contexto Delimitado)

Contextos Delimitados no DDD devem estar atrelados para um problema, e não uma proposta de solução. O foco e a fronteira de um contexto é ditado pelo problema que deseja resolver. Este problema pode conter múltiplas soluções possíveis e, cada proposta de solução pode corresponder para 1 ou mais sistemas.
Defina com clareza o problema principal e os subproblemas.

Ainda sobre Contextos Delimitados, o autor informar que não há uma receita/fórmula a ser aplicada para auxiliar na delimitação de contexto mas, ressalta que há alguma heurística que pode contribuir para esse objetivo.

Uma delas corresponde para o número de propostas de solução existentes para aquele problema. Como cada proposta de solução pode ensejar 1 ou mais sistemas, isso pode ser um indicio de delimitação de contexto para aquele problema.
O autor ainda traz outras heuristicas, tais como: número de pessoas envolvidas naquele contexto, número de relacionamentos/integrações daquele contexto com outras, complexidade da linguagem ubíqua.

Sobre modelagem de um conceito, o autor afirma que deve se tomar muito cuidado em querer abstrair um conceito para ser reaproveitado em mais de um contexto. Não significa que conceitos semelhantes serão sempre semelhantes mas, pode apenas ser um acaso daquele momento.
Quando se pretende abstrair um conceito para reaproveitar em contextos distintos, inevitavelmente você se deparará com atributos opcionais, comportamentos condicionais e complexidade desnecessária.
Exemplo: conceito de usuário.
Sempre que possível, duplique aquele conceito nos respectivos contextos, pois evitará acoplamento e também deixará de ser pego de surpresa por adotar uma abstração prematura.

Entidades, Objetos de Valor e Agregados

Esses itens (Entidades, Objetos de Valor e Agregados) fazem parte do DDD tático, quais são building blocks para materializar os conceitos do domínio.
Uma Entidade é um objeto com identificador único qual permite localizá-lo ao longo do seu tempo d vida, persistí-lo e operar com ele. Um identificador pode ser composto por 1 ou mais campos/propriedades.
Objeto de Valor é reconhecido pela totalidade de suas características, isto é, pelo seu estado, sem possuir um identificador único.
Agregado se faz presente quando há necessidade de garantir invariantes da classe no qual envolve diversas outras classes.
O Agregado se torna centralizados dessas operações, principalmente, quais envolvem outros componentes, para garantir a consistência.

DDD e Frameworks

O autor advoga para seguir um caminho um pouco contraditório em relação ao acoplamento dos componentes táticos do DD (entidades, objetos de valor, agregados) com a tecnologia/framework utilizado, aceitando um pequeno acoplamento desde que o design de código continue coeso e direcionado ao domínio ao invés da infraestrutura.

Aprofundando o conhecimento do domínio

Software é materializar o desejo do software.
Precisa entender.
Nível de Complexidade Cognitiva = Taxonomia de Bloom.

Consegui explicar de maneira detalhada aquilo que está se resolvendo.

O aprofundamento no conhecimento do domínio visa tornar a pessoa mais especialista no assunto. É compreendido em que, quanto maior o seu conhecimento sobre o tema, mais será as chances de conseguir tangibilizar o problema daquele domínio em software.
O aprofundamento passa pelo processo de aprendizagem, qual a teoria atrelada a Taxonomia de Bloom pode ajudar a esclarecer o nível de complexidade cognitiva esperado para aprofundamento no domínio.
Na leitura do autor, o nível mínimo necessário é o Understand (Compreender), onde você é capaz de explicar os conceitos e motivos atrelados aquele domínio.
Dentro da Taxonomia de Bloom, o aprofundamento passará pela absorção das teorias, como forma de encurtar o caminho sobre os conceitos em voga no domínio. Posteriormente, a busca pela prática das teorias absorvidas, seja por meio de tangibilizar o domínio pelo código, da explicação com os especialistas e assim por diante.
E, o último passo é da validação, para se certificar do que aprendeu e praticou se está certo e faz sentido. Isso forma o tripé, mencionado pelo autor, para se mergulhar no domínio proposto.
Então, entender mais do produto/serviço, o motivo pelo qual aquele produto/serviço é necessário para os clientes, explicar o que foi entendido e validar com os especialistas, é uma maneira também em se tornar especialista do tema, para aumentar as chances de conseguir explicar de maneira detalhada aquilo que está se resolvendo.

É incentivado a pró-atividade da pessoa para se aprofundar no conhecimento.

Sacar dos detalhes do produto majoritamente torna-se parte do especialista de domínio, e os especialistas de tecnologia cuidam da implementação desses detalhes. Geralmente há uma fricção, um problema na forma de comunicação, um distanciamento entre as partes.
Esse distanciamento quebra a coesão do trabalho. Aumenta duplicação do trabalho, aumenta a necessidade de alinhamento. Por isso é incentivado os engenheiros de software se tornarem mais especialistas no domínio, qual ajudará a modelar o software orientado ao domínio.
Procurar as fontes teóricas, estudar, recuperar para se certificar do que está entendendo corretamente. Diminuir a distância. Pensar/elaborar um plano de estudos.

Vocabulário/glossário: composto por palavras/termos de negócio d/ou palavras/termos técnicos daquele contexto.
Buscar maximizar as chances de todos utilizarem as mesmas palavras para todos terem o mesmo entendimento.
Precisa exercitar a construção desse vocábulário, exercitar o entendimento desse vocabulário com outras pessoas. Buscar construir vocábulário para o contexto do problema qual tem interesse em resolver.

Contextos Delimitados: problema e sub-problemas complexos
Contexto Delimitado pelo problema, em função da complexidade dele.

Contextos Delimitados: definindo problemas e sub-problemas core.

Design Estratégico contempla Contextos Delimitados.

Problema (desejo): eu quero aumentar cada vez mais o nível de confiabilidade na capacidade técnica das pessoas em desenvolverem código com qualidade independente da situação. Qualidade não é negociável!
    - O problema é código/software são construídos sustentados por código que deixam a desejar regularmente em qualidade sob vários aspectos diferentes, quando pensamos em design, testabilidade e etc.

Para resolver o mesmo problema, várias soluções podem ser propostas! Ter clareza em como endereçar a solução do problema!

Miro

Problema: Equipes de engenharia produzem código cujo design deixa a desejar em multiplos aspectos. Isso acarreta em software com implementações mais complexas do que seriam necessárias, muitas vezes também com implementações mais simples do que a complexidade da situação exige fazendo com que, no final de tudo, a manutenibilidade fique cada vez mais custosa.

Esse problema se divide em outras partes? Devemos atacar ele de uma vez só ou esse problema tem várias outras coisas dentro dele que pode dividir em sub-problemas que são importantes o suficiente para que eles sejam atacados de forma super coesa?

Divisão de Problemas

Problema 1: As equipes não conhecem de fato seu próprio nível. Ninguém tem uma combinação de evidências que falem com propriedade sobre a capacidade técnica das pessoas que trabalham ali.

Problema 2: As equipes não conseguem estudar com eficiência, focadas em de fato melhorar as habilidades que são necessárias para o dia a dia do trabalho.

Você tem um determinado problema em função da principal coisa que você entende que é o principal problema, você tem sub-problemas que você precisa resolver que dentro deles tem um conjunto de informações, de características tão coesas, que você consegue descrever esse problema novamente e consegue visualizar diversas ações ali dentro.

Vai precisar de pessoas o tempo inteiro pensando no espaço desse problema. Pessoas pensando em problema que se conecta com o problema principal.

Fatores:
    - existem maneiras (ou maneiras complementares) de atacar aquele problema que eu estou definindo?
        - problema 1: as equipes não conhecem de fato seu próprio nível
            - se auto avaliar
            - responder provas teóricas em relação ao que está sendo exposto
            - avaliação de pares
            - avaliação de estudo para se certificar se está se aproximando do seu objetivo de estudo (autorregulação)
            -- todos os itens acima ajudam a pessoa a identificar em como está indo, como está seu progresso.

Fator/motivo

Quando existem N maneiras de se atacar aquele mesmo problema, parece que aquilo é grande o suficiente para ser um contexto delimitado. Representa uma força de coesão. No exemplo do Problema 1, as N maneiras de se atacar o problema correspondem para AVALIAR, sobre avaliação.

        - problema 2: as equipes não consegue estudar com eficiência
            - consumir teoria para saber o que fazer
            - praticar de diferentes maneiras para conseguir aplicar aquela teoria de maneira interessante (não somente código, nas palestras, explicar coisas dentro da empresa)
            - consumir teoria em mídias diferentes, formatos diferentes
            - práticas complexas, variabilidade da prática.

OBS: Isso não tem relação em COMO VAI RESOLVER. As mesmas N maneiras de atacar o problema não são sinônimo sobre como será resolvido aquele problema.

Fatore(s):
    - equipes(s)