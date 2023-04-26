---
title: "OAuth 2.1 Flows"
date: 2023-04-26T06:47:00-03:00
tags: [oauth]
---

For the OAuth 2.1, the amount of recommended flows decreased (from 5 to 2), in which they are:

- Client Credentials
- Authorization Code with PKCE

## Client Credentials

That flow represents the machine to machine communication, in which you don't have "interactive" user present or, at least, you don't care about it. It means that the user information is not necessary to get resources access, only the client information.

The client sends a POST request to the _token_ endpoint in Authorization Server. For successful request, the cliente receives an access token in the response so that, it is able to consume the resources available in Resource Server.

The protocol doesn't define the token format because there is a trust relationship between Authorization Server and Resource Server, even that JWT token is commonly used in the OAuth scenarios nowadays, the format is interested only for Authorization and Resource servers.

The API (Resource Server) must validate the token signature. Besides that, others information must be validated, such as:

- the issuer must has the expected value even though it exists in the signature, due to multi-tenancy scenarios (Azure AD, for example)
- algorithm type
- current time
- scope

## Authorization Code with PKCE

This flow is divided into 2 parts:

- Front-Channel
- Back-Channel

### Front-Channel

The public client will communicate to Authorization Server and use the successful response on it (the code provided by the callback in the request parameter __redirect_uri__) to delegate to its Back-Channel. The user (or an attacker) will never see from the device the access token has been passed by to the Resource Server.

The information are send using HTTP's _query parameters_ to the _authorize_ endpoint. One of the parameters is __response_type__ in which the value is _code_ (it represents the Authorization Code flow). Another one we can mentioned is __code_challenge__.

The client doesn't know how the user is authenticated in the Authorization Server. When it is necessary authenticate user in interactive apps (browser, for example), thinking about the idea to centralize the authorization service, the authentication page showed to browser belongs to Authorization Server. It shows its Authentication page and if it would be succeeded, the Authorization Server will use the __redirect_uri__ parameter sent by the client to provide the authentication result (the code).

In this approach, the user will face with Consent page to grant necessary access the client is intended to use.

### Back-Channel

That's the part where the client is considered as a confidential one to communicate to Authorization Server to get the access token. It is also responsible to deal with OAuth libraries, token management and session management (safer place to implement all of those stuffs).

The client sends request to token endpoint using __authorization_code__ grant type. It is a HTTP POST request, in which also sending code (got from Front-Channel), the __redirect_uri__ and the __code_verifier__. The code verifier has the purpose to tell to Authorization Server that it has been created by the client just for this request. It is a mechanism introduced by mobile apps because there is no central registry for these custom schemes so the rogue app can register the callback URL of a legitime app and steal the code.

However, with code verifier to redeem the token you need to have it, in which is a one-time password the client application came up with, the Server Authorization will response if the hash matched for the provided code.