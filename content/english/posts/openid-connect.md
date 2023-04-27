---
title: "OpenID Connect"
date: 2023-04-27T07:23:50-03:00
tags: [openid-connect]
---

OpenID Connect is an extra layer on top of OAuth, so we can say it has the same flows that OAuth has with few more scopes to extend it.

So, when we talk about the access token, the protocol says it must not used by the client to read and get access for its information. Clients only need to forward it. On the other hand, clients maybe need to get user information, therefore, OpenID Connect provides the identity token in which only the clients will use it.

In a nutshell:

- Access token: client only forward it to Resource Server
- Identity token: client only read it to get user information

OpenID Connect response will contain the _id\_token_. Again, the consumption must be only by the client. This token should never forwarded to the API (Resource Server). It has the _aud_ claim in its payload to reference the client will consume it.