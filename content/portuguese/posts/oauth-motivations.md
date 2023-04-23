---
title: "Motivação para o OAuth"
date: 2023-04-23T13:35:47-03:00
tags: [oauth]
slug: "motivacoes-oauth"
---

No ano de 2005 surgiu o primeiro protocolo utilizando tecnologias web para fornecer autenticação e autorização com provedor de identidade: SAML 2.0.

Antes era possível fazer isso em aplicações web com tecnologias NTLM ou Kerberos colocando-as dentro do navegador para ter acesso aos recursos usando o Active Directory, por exemplo, como forma de ter single sign-on nessas aplicações.

No entanto, a ideia com o SAML 2.0 era sobre como poderíamos provar que o usuário é o usuário fazendo requisições pelo navegador? Para as tecnologias dessa época, estamos falando sobre o uso de SOAP (XML) e seus padrões de assinatura (assinatura XML).

Pouco tempo depois do SAML 2.0, surgiu a necessidade de usar essa abordagem (single sign-on) com tecnologias modernas no navegador (JSON, javascript e assim por diante), mas o SAML 2.0 é executado no lado do servidor e na maioria das vezes reconhecido como solução enterprise, ou seja, rodando em um ambiente conhecido e controlado pela empresa.

Foi nessa época que o OAuth apareceu para redefinir o uso das APIs para essa abordagem em navegadores (e outros tipos de clientes que geralmente conhecemos hoje em dia).
Desde a especificação original para OAuth 2.0 (podemos considerar até mesmo a especificação para OAuth 1.0) até OAuth 2.1, existem algumas recomendações feitas no passado que não fazem mais sentido na versão 2.1, tornando o protocolo mais simples de entender e mais seguro também.

A ideia com OAuth na internet é usar APIs HTTP para que você não enfrente problemas de compatibilidade no cenário onde 2 partes possuem tecnologias diferentes que podem dificultar a integração como WS-Security e outras abordagens similares nessa época.

Para se comunicar com uma API, usamos uma chave de API, ou seja, a senha da API. No entanto, o cliente precisa enviar a chave da API para cada requisição e talvez para APIs diferentes, onde existe o risco de a senha ser logada (falha de segurança), portanto, a ideia de usar um token de curta duração pode minimizar os impactos nesse cenário.
Token com janela de tempo é uma abordagem usada desde o SAML 2.0.

## Token

- __Emissor__: Quem disse isso sobre o usuário? Quem garante esse usuário?
- __Assinatura__: Para comprovar que o token é emitido pelo emissor e mais ninguém.
- __Janela de Tempo__: Por quanto tempo este token é válido?
- __Escopo__: significa indicar que o token não é válido para qualquer lugar, é válido para APIs específicas.
- __Informações sobre a autenticação__: Como foi feita esta autenticação?
- __Claims__: São pares chave-valor e uma maneira flexível de fornecer informações que a API possa precisar.

O conceito em OAuth: um cliente pode fazer requisições em nome de alguém (usuário, por exemplo).

## Clientes OAuth

Temos clientes públicos e confidenciais. A diferença entre eles é que os clientes confidenciais, nos quais você terá comunicação servidor a servidor, são capazes de armazenar segredos de forma segura que não é tão fácil para um invasor usar uma ferramenta ou outro meio para obter essas informações de suas configurações. 

Por outro lado, os clientes públicos, nos quais você terá aplicativos de browsers ou de dispositivos se comunicando com o servidor de identidade, permitem que o usuário (ou um invasor) obtenha informações mais facilmente nesses dispositivos em que os segredos podem ser armazenados (como ferramentas de desenvolvimento), abrindo um oportunidade para outra pessoa se passar por alguém ou logar o token da API ao enviar uma requisição para uma API (servidor de recursos) com esse token.

## Identidade Central

No OAuth, a ideia é que a senha seja enviada junto com a requisição apenas para o Servidor de Autorização. Você não verá requisições com senha de usuário enviadas para qualquer outro lugar (como o Servidor de Recursos) porque o Servidor de Autorização e o Servidor de Recursos confiam um no outro. Além disso, a ideia é que ninguém mais precise saber a senha do usuário ou o método de autenticação, exceto o emissor (quem está guardando as informações do usuário).

Isso pressupõe, para o fluxo do código de autorização do OAuth, por exemplo, que o Servidor de Autorização que fornecerá o mecanismo de autenticação para o cliente (página de login, por exemplo).

Quando o cliente envia requisições de autorização, ele também envia o parâmetro __scope__ para perguntar quais APIs o cliente tenta acessar. Este é um parâmetro necessário. Por exemplo, se o cliente precisar obter acesso à API de calendário do Google, o cliente solicitará ao Servidor de Autorização em nome de alguém (novamente, o proprietário do recurso) para obter acesso ao Google Calendar no parâmetro __scope__.