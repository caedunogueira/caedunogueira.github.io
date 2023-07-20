---
title: "Components do IAM no Azure"
date: 2023-07-20T18:49:21
tags: [azure]
slug: "components-do-iam-no-azure"
---

Existem 3 componentes usados para a Gestão de Autorização de Identidades do Azure:

- _Azure Active Directory_
- _Azure Role-Based Control_
- _Scopes_

## Azure Active Directory

Pertence ao topo da hierarquia de recursos, na qual identifica e comprova que você é quem diz ser. Depois que a identidade for resolvida, o papel e as permissões podem ser definidas para essa identidade. Cada identidade no Azure é conhecida como _security principal_ porque a identidade pode representar usuários, aplicativos e assim por diante.

## Azure Role-Based Control (Azure RBAC)

Ele fornece gerenciamento de acesso mais granular aos recursos do Azure.
Papel (_role_) é uma coleção de permissões individuais. Permissões individuais, por exemplo, como criar máquinas virtuais, visualizar máquinas virtuais e outros exemplos semelhantes a esse. Um pacote de permissões individuais é atribuído a um papel.
O papel é atribuída para _security principal_.

## Scopes

_Scopes_ é um conjunto de recursos para conceder acesso e tem relação direta com a hierarquia de recursos.