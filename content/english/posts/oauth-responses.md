---
title: "OAuth Responses"
date: 2023-04-26T07:24:26-03:00
tags: [oauth]
---

When there is a problem with authorization, there are 2 HTTP response status code used to let the client know a little bit more about the problem:

## 401 - Unauthorized

The Resource Server can answers for one of the 2 scenarios:

- We don't know who you are
- We won't accept anymore your token because it is expired

## 403 - Forbidden

The Resource Server answers for the scenario:

- We know perfectly you are but you are not allowed to get access for this resource