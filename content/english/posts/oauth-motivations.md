---
title: "Motivations to OAuth"
date: 2023-04-23T13:35:47-03:00
tags: [oauth]
---

In the year of 2005 came up the first protocol using web technologies to provide authentication and authorization with identity provider: SAML 2.0.

Before that, it was feasible to do that in web applications with NTLM or Kerberos technologies putting those inside the browser to get access to resources using Active Directory, for example, as a way to have single sign-on on those applications.

However, the idea with SAML 2.0 was in how could we proof the user is the user by doing requests to the browser? For those technologies in that age we are talking about use of SOAP (XML) and its signature standards (XML signature).

A little time after SAML 2.0, came up the need to use that approach (single sign-on) with modern technologies on the browser (JSON, javascript and so on) but SAML 2.0 run in the server-side and most of the time recognized as a closed enterprise solution, it means, running in a knowing and controlled environment by the company.

That was the time OAuth appeared to redefined use of the APIs for that approach in browsers (and other types of clients we generally know of them nowadays).
From the original spec for OAuth 2.0 (we might consider even the spec for OAuth 1.0) to OAuth 2.1, there are some recommendations made in the past that they don't make sense anymore in version 2.1, becoming the protocol simpler to understand and more secure too.

The ideia with OAuth on the internet is using HTTP APIs so you won't face with compatibility problems in the scenario where 2 parts has different stacks that could difficult the integration as WS-Security and other similar approachs in that age.

To communicate to an API we use an API key, it means the API password. However, the client needs send the API key to each request and maybe to different APIs, where there is a risk that password could be logged (security fault) so, the idea of use a short-lived token could minimize the impacts in this scenario.
Token with time window is an approach used since SAML 2.0.

## Token

- __Issuer__: Who said this about the user? Who vouches about this user?
- __Signature__: To proof that the token issued by the issuer and no one else.
- __Time Window__: How long this token is valid?
- __Scoping__: it means to indicate the token is not valid to anywhere, it is valid for specific APIs.
- __Information about the authentication__: How this authentication was done?
- __Claims__: They are a key-value pairs and a flexibe way to provide information that API might need.

The concept in OAuth: a client are able to make requests in behalf of someone (user, for example).

## OAuth Clients

We have public clients and confidencial ones. The difference between them is the confidencial clients, in which you will have server to server communication, are able to store secrets ina  secure way that it's not so easy to an attacker use a tool or other mean to get that information from its configs. 

On the other hand, public clients, in which you will have browsers or devices applications communicating to identity server, allow the user (or an attacker) to get information easier in those devices the secrets could be stored (like dev tools), opening an opportunity to someone else impersonate someone or log the API token when sending request to an API (Resource Server) with that token.

## Central Identity

In OAuth, the idea is that the password sending along to the request only to Authorization Server. You won't see requests with user password sending to anywhere else (like Resource Server) because the Authorization Server and Resource Server trust on each other. Besides that, the idea is anyone else don't need to know the user password or the authentication method except the issuer (who is keeping the user information).

This assumes the OAuth's Authorization Code flow, for example, the Authorization Server provides the authentication mechanism for the client (login page, for example).

When client send authorization requests, it also send the __scope__ parameter to ask what APIs the client tries to reach. This is necessary parameter. For example, if the client needs to get access to Google's Calendar API, the client asks Authorization Server in behalf of someone (again, resource owner) to get access Google Calendar in the __scope__ parameter.