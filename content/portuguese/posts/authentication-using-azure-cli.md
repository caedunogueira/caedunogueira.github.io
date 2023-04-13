---
title: "Autenticação usando  Azure CLI"
date: 2023-04-03T07:01:45-03:00
slug: "autenticacao-usando-azure-cli"
---

Há duas formas com propósito de se autenticar na Azure usando Azure CLI:

- Modo Interativo
- Modo Entidade de Serviço

## Modo Interativo

```sh
az login
```

Permite você autenticar na Azure abrindo uma página de autenticação do portal no browser para manualmente fornecer o usuário e senha.

## Modo Entidade de Serviço

```sh
az login --service-principal
```

É ideal para cenários usados por ferramentas de automação. Você irá criar uma entidade de serviço (se ainda não existe) ou pelo comando `az ad sp create` ou pelo comando `az ad sp create-for-rbac`, dando por último as permissões apropriadas para os recursos na Azure.
Ao invés de conceder acesso completo para essas ferramentas é recomendavél utilizar a entidade de serviço com permissões restritivas.
O parâmetro `--service-principal` deve ser fornecido com outros para autenticar dessa forma.