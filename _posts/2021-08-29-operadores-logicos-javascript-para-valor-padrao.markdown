---
layout: single
title: Operadores lógicos em Javascript para definir valor padrão
date: 2021-08-29 14:50:00 -0300
categories: programacao
tags: javascript AND OR padrão default
---

Em alguns momentos, espera-se que uma variável contenha algum valor de determinado tipo, dessa forma para compor outras expressões/instruções no que tange alcançar o resultado proposto naquele fragmento de código.

No cenário em que a variável não possui tal valor, é possível atribuir um valor padrão com o auxílio de uma instrução condicional como **if**, por exemplo:

```javascript
function setNumber(value) {
    if (!value)
        return 10;
    
    return value;
}

let myNumber1 = setNumber(0);
let myNumber2 = setNumber(15);

console.log(`myNumber1: ${myNumber1}`);
console.log(`myNumber2: ${myNumber2}`);

// resultado
// myNumber1: 10
// myNumber2: 15
```

Além do exemplo acima, dentre outras opções para alcançar o mesmo resultado, uma delas é a utilização dos operadores lógicos **AND** e **OR**. Abaixo é demonstrado um exemplo com operador **OR**:

```javascript
const setNumber = (value) => value || 10;

let myNumber1 = setNumber(0);
let myNumber2 = setNumber(15);

console.log(`myNumber1: ${myNumber1}`);
console.log(`myNumber2: ${myNumber2}`);

// resultado
// myNumber1: 10
// myNumber2: 15
```

Os operadores **AND** e **OR**, quando utilizados dessa forma, tratam de realizar a conversão do valor localizado a sua esquerda em valor boleano. 

Para o tipo **string**, quando uma string é vazia, a conversão resultará em _false_, caso contrário será _true_. Já para o tipo **number**, os valores _0_ e _NaN_ resultarão em _false_ enquanto os demais serão _true_.
Em variáveis com valor vazio (_undefined_ ou _null_), a conversão resultará em _false_.

Para o operador **OR**, a escolha pelo valor a esquerda ocorrerá se a sua conversão resultar em _true_. Caso contrário, escolherá o valor a sua direita.

Já para o operador **AND**, a escolha pelo valor a esquerda ocorre pelo motivo oposto. O valor a esquerda ocorrerá se a conversão resultar em _false_. Caso contrário, escolherá o valor a direita.

Como os operadores lógicos utilizam a abordagem de short-circuit, uma vez que o valor a sua esquerda atenda aos requisitos (_true_ para **OR** e _false_ para **AND**) o valor a sua direita não é nem mesmo avaliado.

Referência: [Eloquent Javascript](https://eloquentjavascript.net/)