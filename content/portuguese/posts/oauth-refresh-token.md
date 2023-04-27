---
title: "Refresh Token"
date: 2023-04-27T07:02:00-03:00
tags: [oauth]
slug: "refresh-token-oauth"
---

O _refresh token_ é um token de referência, portanto, você pode revogá-lo se alguém o roubar. Como token de referência, o protocolo o define como de longa duração. Se você removê-lo do armazenamento do Servidor de Autorização, o invasor não poderá obter um novo token de acesso novamente. O Servidor de Autorização pode fornecer uma lista de aplicativos aprovados pelo usuário (e que podem ser revogados).

O caso de uso usual é a sessão de duração (renovar o token de acesso obtendo um novo sem fornecer as credenciais novamente).

Quando o usuário fizer logout, é recomendável revogar o _refresk token_ devido ao término da sessão (endpoint _revoke_).