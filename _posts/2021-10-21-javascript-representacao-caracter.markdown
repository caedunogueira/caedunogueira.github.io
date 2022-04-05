---
layout: single
title: "Javascript: representação de caracteres"
date: 2021-10-21 08:20:00
categories: programacao
tags: javascript unicode utf-16
---

Toda informação a ser interpretada pela máquina é processada na forma de bits (0 e 1). Com string não é diferente. Para cada caracter em uma string, há um conjunto de bits e consequentemente podemos ter um código decimal correspondente a esse conjunto.

Há algumas tabelas de caracteres que permitam deduzir para determinado código decimal, qual o caracter correspondente. Essas tabelas variam de acordo com a quantidade de bits que um caracter utiliza e umas das mais utilizadas (ou a mais utilizada) é referente ao **Unicode**.

Em Javascript, todos os caracteres armazenados são encontrados na tabela Unicode. Seu armazenamento segue o padrão **UTF-16**, que faz uso de um par de _code units_ (unidades de código) de 16 bits cada. A maioria dos caracteres que utilizamos (em nosso idioma, por exemplo) precisa apenas de uma unidade de 16 bits para representá-los. Com uma unidade de 16 bits, pode-se reconhecer um pouco mais de 63.000 caracteres.
Contudo, Unicode possui uma quantidade de caracteres significativamente maior, onde uma unidade não é o suficiente, como caracteres de emoji, por exemplo (que são representados por um par de unidades).

Ao percorrer os caracteres de uma string em Javascript, para identificar o código correspondente na tabela Unicode, pode-se utilizar o método `codePointAt(0)`.

Abaixo segue um exemplo:

```javascript
let myText = "Carlos 😁 hoje";
for (let char of myText)
  console.log(`Para o caracter ${char} seu código é: ${char.codePointAt(0)}.`);

// resultado
// Para o caracter C seu código é: 67.
// Para o caracter a seu código é: 97.
// Para o caracter r seu código é: 114.
// Para o caracter l seu código é: 108.
// Para o caracter o seu código é: 111.
// Para o caracter s seu código é: 115.
// Para o caracter   seu código é: 32.
// Para o caracter 😁 seu código é: 128513.
// Para o caracter   seu código é: 32.
// Para o caracter h seu código é: 104.
// Para o caracter o seu código é: 111.
// Para o caracter j seu código é: 106.
// Para o caracter e seu código é: 101.
```

Referência: [Eloquent Javascript](https://eloquentjavascript.net/)