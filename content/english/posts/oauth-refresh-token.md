---
title: "Refresh Token"
date: 2023-04-27T07:02:00-03:00
tags: [oauth]
---

Refresh token is a reference token so, you can revogate it if someone stole from you. As a reference token the protocol define it to a long-lived. If you remove it from Authorization Server storage the attacker won’t be able to get a new access token again. The Authorization Server can provide a list of apps approved by the user (and that can be revogate).

The usually use case is the duration session (renew the access token getting a new one without provide the credentials again).

When the user logout, it is recommended to revoke the refresh token due to the session finished (_revoke_ endpoint).