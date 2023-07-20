---
title: "Hierarquia de Recursos no Azure"
date: 2023-07-20T12:19:55
tags: [azure]
slug: "hierarquia-de-recursos-no-azure"
---

Existe uma organização de recursos no Azure aplicada em 5 níveis, tais como:

- _Tenant_
     - _Management Group_
         - Assinaturas
             - Grupo de Recursos
                 - Recursos

Uma das vantagens dessa organização é uma maneira centralizada de configurar permissões. As permissões aplicadas em um nível serão replicadas para os níveis inferiores. Por exemplo, a política de acesso estabelecida para um conjunto de identidades e papéis para uma assinatura específica significa que todos os recursos pertencentes a ela estarão em conformidade com essas políticas. Para manter essa política, modificar em um local replicará as alterações em todos os recursos disponíveis nessa assinatura.
A autorização centralizada pode ser aplicada para todos os níveis.

## Tenant

Tenant é uma única instância que representa a organização, como Microsoft, McDonalds, Warner Bros e assim por diante. O _tenant_ é o nível superior da hierarquia e contém todos os diretórios de usuários ou diretórios de identidades que a empresa dará permissão específica para alguns recursos do Azure.

## Management Group

O objetivo do _Management Group_ é centralizar várias assinaturas em um só lugar. Não é obrigatório usar o _Management Group_ mas, uma vantagem, além de organizar as assinaturas, é o benefício de usar a autorização centralizada na qual você pode aplicar a mesma política de acesso para algumas assinaturas ao mesmo tempo.

## Assinaturas

A assinatura é um componente que representa o contrato de pagamento escolhido para pagar o uso dos recursos do Azure. Cada assinatura tem seu próprio contrato de cobrança.

## Grupo de Recursos

Como boa prática, para manter juntos todos os recursos pertencentes ao mesmo projeto ou pertencentes ao mesmo ciclo de vida, o Grupo de Recursos é uma maneira de fazer isso.

## Recursos

Eles são máquinas virtuais, serviços de armazenamento, redes e assim por diante.