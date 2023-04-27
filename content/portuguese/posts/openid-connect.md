---
title: "OpenID Connect"
date: 2023-04-27T07:23:50-03:00
tags: [openid-connect]
---

O OpenID Connect é uma camada extra sobre o OAuth, então podemos dizer que ele tem os mesmos fluxos que o OAuth tem com mais alguns escopos para estendê-lo.

Então, quando falamos do token de acesso, o protocolo diz que ele não deve ser usado pelo cliente para ler e obter acesso às suas informações. Os clientes só precisam encaminhá-lo. Por outro lado, os clientes podem precisar obter informações do usuário, portanto, o OpenID Connect fornece o token de identidade no qual apenas os clientes o usarão.

Em poucas palavras:

- Token de acesso: o cliente apenas o encaminha para o servidor de recursos
- Token de identidade: o cliente apenas o lê para obter informações do usuário

A resposta do OpenID Connect conterá o _id\_token_. Novamente, o consumo deve ser apenas do cliente. Este token nunca deve ser encaminhado para a API (Servidor de Recursos). Ele tem a claim _aud_ em seu payload para fazer referência ao cliente que o consumirá.