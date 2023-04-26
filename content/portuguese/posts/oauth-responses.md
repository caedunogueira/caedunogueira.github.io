---
title: "Respostas do OAuth"
date: 2023-04-26T07:24:26-03:00
tags: [oauth]
slug: "respostas-oauth"
---

Quando há um problema de autorização, existem 2 códigos de status de resposta HTTP usados para informar o cliente um pouco mais sobre o problema:

## 401 - Não Autorizado

O Servidor de Recursos pode responder para um dos 2 cenários:

- Não sabemos quem você é
- Não aceitaremos mais seu token porque ele expirou

## 403 - Proibido

O Servidor de Recursos responde para o cenário:

- Sabemos perfeitamente que você é mas, você não tem permissão para acessar este recurso