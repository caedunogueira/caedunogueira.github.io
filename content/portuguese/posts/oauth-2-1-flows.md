---
title: "Fluxos do OAuth 2.1"
date: 2023-04-26T06:47:00-03:00
tags: [oauth]
slug: "fluxos-oauth-2-1"
---

Para o OAuth 2.1, a quantidade de fluxos recomendados diminuiu (de 5 para 2), sendo eles:

- Credenciais do Cliente
- Código de Autorização com PKCE

## Credenciais do Cliente

Esse fluxo representa a comunicação máquina a máquina, na qual você não tem um usuário "interativo" presente ou, pelo menos, não se importa com isso. Isso significa que as informações do usuário não são necessárias para obter acesso aos recursos, apenas as informações do cliente.

O cliente envia uma requisição POST para o endpoint _token_ no Servidor de Autorização. Para uma requisição bem-sucedida, o cliente recebe um token de acesso na resposta para que possa consumir os recursos disponíveis no Servidor de Recursos.

O protocolo não define o formato do token porque existe uma relação de confiança entre o Servidor de Autorização e o Servidor de Recursos, mesmo que o token JWT seja comumente usado nos cenários OAuth hoje em dia, o formato interessa apenas para os servidores de Autorização e Recursos.

A API (Servidor de Recursos) deve validar a assinatura do token. Além disso, outras informações devem ser validadas, tais como:

- o emissor deve ter o valor esperado, mesmo que exista na assinatura, devido a cenários de _multi-tenacy_ (Azure AD, por exemplo)
- tipo de algoritmo
- hora atual
- escopo

## Código de Autorização com PKCE

Este fluxo é dividido em 2 partes:

- _Front-Channel_
- _Back-Channel_

### Front-Channel

O cliente público se comunicará com o Servidor de Autorização e usará a resposta bem-sucedida nele (o código fornecido pelo _callback_ no parâmetro da requisição __redirect_uri__) para delegar ao seu Back-Channel. O usuário (ou um invasor) nunca verá no dispositivo que o token de acesso foi passado para o servidor de recursos.

As informações são enviadas usando _query parameters_ do HTTP para o endpoint _authorize_. Um dos parâmetros é o __response_type__ em que o valor é _code_ (representa o fluxo do Código de Autorização). Outro que podemos mencionar é __code_challenge__.

O cliente não sabe como o usuário é autenticado no Servidor de Autorização. Quando for necessário autenticar o usuário em aplicativos interativos (navegador, por exemplo), pensando na ideia de centralizar o serviço de autorização, a página de autenticação apresentada no navegador pertence ao Servidor de Autorização. Ele mostra sua página de Autenticação e se for bem-sucedido, o Servidor de Autorização usará o parâmetro __redirect_uri__ enviado pelo cliente para fornecer o resultado da autenticação (o código).

Nessa abordagem, o usuário se deparará com a página de consentimento para conceder o acesso necessário que o cliente pretende usar.

### Back-Channel

Essa é a parte em que o cliente é considerado confidencial para se comunicar com o Servidor de Autorização para obter o token de acesso. Também é responsável por lidar com bibliotecas OAuth, gerenciamento de token e gerenciamento de sessão (local mais seguro para implementar todos esses itens).

O cliente envia a requisição para o endpoint _token_ usando o tipo de concessão __authorization_code__. É uma requisição HTTP POST, na qual também estão sendo enviados o código (obtido do Front-Channel), o __redirect_uri__ e o __code_verifier__. O verificador de código tem a função de informar ao Servidor de Autorização que ele foi criado pelo cliente apenas para esta requisição. É um mecanismo introduzido por aplicativos móveis porque não há registro central para esses esquemas personalizados, de modo que o aplicativo não autorizado pode registrar o URL de retorno de chamada de um aplicativo legítimo e roubar o código.

Contudo, com o verificador de código para resgatar o token, você precisa tê-lo, que é uma senha de uso único que o aplicativo cliente criou, a autorização do servidor responderá se o hash corresponder ao código fornecido.