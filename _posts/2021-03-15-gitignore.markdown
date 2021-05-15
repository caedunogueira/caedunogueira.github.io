---
layout: single
title: "Ignorar arquivos e/ou diretórios no Git"
date: 2021-03-15 08:10:00 -0300
categories: controle-versao
tags: git
---

Há arquivos e/ou diretórios que é desejado não pertencerem ao histórico de versões do repositório, por exemplo, arquivos de compilação. Um caminho seria excluir tais itens ao fazer uso toda vez do comando `git add`. Contudo, isso provavelmente seria tedioso, não somente pela quantidade de vezes ao utilizar o comando (que serão muitas) ou a quantidade de arquivos e/ou diretórios a serem ignorados mas principalmente porque está sujeito a falhas (em um determinado momento a pessoa pode esquecer de ignorá-los na seleção para a Staging Area).

Uma forma mais prática de **ignorar** tais itens, pelo Git, é utilizar o arquivo _.gitignore_.

É possível indicar quais itens do repositório ignorar para a adição na Staging Area por meio desse arquivo. É utilizado um padrão GLOB (pelo que é dito na referência, uma forma simplificada de expressão regular) para selecionar os itens do  repositório que serão ignorados. Tal configuração surte efeito somente para itens _não rastreados_, isto é, se um item não desejado encontra-se na Staging Area ou em algum commit, as configurações do _.gitignore_ não surte efeito.

O arquivo _.gitignore_ geralmente é adicionado na raiz do repositório. O `*` pode ser utilizado para indicar que independente de qual ou quais caracteres a partir daquela posição existem, itens devem ser ignorados. Por exemplo: teste-* ignorará todos os arquivos/diretórios que existam tais como: _teste-teste1_, _teste-teste2_, _teste-teste3_ e assim por diante.

Com `?` é possível indicar em dada posição daquele texto ignorar todos os caracteres. Por exemplo: n?mes ignorará arquivos/diretórios como _nomes_, _names_, e qualquer outro caractere que esteja na segunda posição. A diferença entre `?` e `*` é que o primeiro exige que um caractere naquela posição exista, ao contrário do segundo. Caso, ao invés de todo caractere, opte por ignorar somente um conjunto deles, pode ser utilizado `[]`. Por exemplo: n[ao]mes ignorará arquvos/diretórios como _nomes_, _names_ mas não _numes_, _nimes_ ou qualquer outro caractere que não esteja entre os colchetes.

Quando é desejado ignorar um subdiretório, basta indicar como `/subdiretorio` ou `subdiretorio` ou `subdiretorio/*`. Ele desconsiderá todos os arquivos daquele subdiretório porém se o mesmo possuir outros diretórios, esses últimos serão considerados. Para também desconsiderar todos os níveis abaixo daquele subdiretório, pode ser utilizado a opção `subdiretorio/**/*`. Nesse contexto, uma variação de opções está disponível para a pessoa aplicar sobre o que deve ser ignorado, como ignorar um conjunto de arquivos no subdiretório (por exemplo, `subdiretorio/*.txt`) ou ignorar a partir de todos os níveis (por exemplo, `subdiretorio/**/*.txt`).

Há também a possibilidade de criar exceções em relação a algumas regras criadas (quando analisado de cima para baixo), com o uso do caractere `!`. Ao utilizar o exemplo abaixo:

```
*.abc
!teste.abc
```

Temos como primeira configuração que todos os arquivos com extensão _abc_ devem ser ignorados. Contudo, se existir um arquivo nomeado `teste.abc`, será considerado pelo Git exceção em relação a regra anterior, portanto, aparecerá como arquivo não rastreado pelo comando `git status`.

Referência: [Git - Book](https://git-scm.com/book/en/v2)