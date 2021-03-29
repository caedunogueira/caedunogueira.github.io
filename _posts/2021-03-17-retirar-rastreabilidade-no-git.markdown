---
layout: single
title: "Retirar rastreabilidade no Git"
date: 2021-03-17 06:50:00 -0300
categories: controle-versao
tags: git remover rastreabilidade
---

Pode haver uma situação que um item (arquivo ou diretório) tenha sido adicionado para o repositório sem necessidade e deseja-se retirá-lo mas não necessariamente excluí-lo do diretório de trabalho. Como exemplo citado [aqui]({{ site.url }}{{ site.baseurl}}/controle-versao/gitignore/index.html), podemos pensar em um cenário que binários do projeto foram adicionados.
{: style="text-align:justify;"}

Os binários deveriam ser ignorados mas como estão rastreáveis, a configuração no arquivo _.gitignore_ não surtirá efeito. Para retirar a rastreabilidade desses arquivos, pode ser feito uso do comando abaixo:
{: style="text-align:justify;"}

```bash
git rm --cached [item]
```

O comando `git rm` combinado com a opção `--cached` adicionará esse item na Staging Area como deletado mas permanecerá no seu diretório de trabalho como **não rastreado**. A partir do próximo comando `git commit` o Git não gerará mais uma versão para aquele arquivo nos próximos snapshots. A imagem abaixo é um exemplo com o arquivo _README_:
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/retirado-rastreabilidade-arquivo-git.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/retirado-rastreabilidade-arquivo-git.JPG" alt="Arquivo sem rastreabilidade e que permanece no diretório de trabalho">
    </a>
</figure>

<figure>
    <a href="{{ site.url }}{{ site.baseurl }}/assets/images/retirado-rastreabilidade-arquivo-git-parte2.JPG">
        <img src="{{ site.url }}{{ site.baseurl }}/assets/images/retirado-rastreabilidade-arquivo-git-parte2.JPG" alt="Arquivo sem rastreabilidade e que permanece no diretório de trabalho - Parte 2">
    </a>
</figure>

O arquivo ainda existe no diretório de trabalho. Dessa forma, pode ser configurado no _.gitignore_ para começar a ser ignorado.
{: style="text-align:justify;"}

<figure>
    <a href="{{ site.url}}{{ site.baseurl }}/assets/images/arquivo-nao-rastreavel-ignorado.JPG">
        <img src="{{ site.url}}{{ site.baseurl }}/assets/images/arquivo-nao-rastreavel-ignorado.JPG" alt="Arquivo não rastreado sendo ignorado">
    </a>
</figure>

**Obs**: Ao não utilizar a opção `--cached` o comando `git rm` removerá não somente do repositório como também do diretório de trabalho.
{: style="text-align:justify;"}

Referência: [Git - Book](https://git-scm.com/book/en/v2)