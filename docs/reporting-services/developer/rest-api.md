---
title: Desenvolver com as APIs REST para o Reporting Services | Microsoft Docs
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
ms.date: 10/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 7c2c34047ac316045387b036cf10ee149175580a
ms.contentlocale: pt-br
ms.lasthandoff: 10/20/2017

---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>Desenvolver com as APIs REST para o Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 2017 Reporting Services oferece suporte a REST Representational State Transfer () APIs. As APIs REST são pontos de extremidade de serviço que suporte a um conjunto de operações de HTTP (métodos), que fornecem criar, recuperar, atualizar ou excluir acesso para recursos em um servidor de relatório.

A API REST fornece acesso programático aos objetos em um catálogo de servidor de relatório do Reporting Services do SQL Server de 2017. Exemplos de objetos são pastas, relatórios, KPIs, fontes de dados, conjuntos de dados, planos de atualização, assinaturas e muito mais. Usando a API REST, você pode, por exemplo, navegar na hierarquia de pasta, descobrir o conteúdo de uma pasta ou baixar uma definição de relatório. Você também pode criar, atualizar e excluir objetos. Exemplos de como trabalhar com objetos são carregar um relatório, executar um plano de atualização, excluir uma pasta e assim por diante.

## <a name="components-of-a-rest-api-requestresponse"></a>Componentes de uma solicitação/resposta de API REST

Um par de solicitação/resposta de API REST pode ser separado em cinco componentes:

* O **URI de solicitação**, que consiste: `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`. Embora o URI de solicitação é incluída no cabeçalho da mensagem de solicitação, vamos chamá-la separadamente aqui porque a maioria dos idiomas ou estruturas exigem que você passá-lo separadamente da mensagem de solicitação.

    * Esquema de URI: indica o protocolo usado para transmitir a solicitação. Por exemplo, `http` ou `https`.
    * Host URI: Especifica o nome de domínio ou endereço IP do servidor onde o ponto de extremidade do serviço REST está hospedado, como `myserver.contoso.com`.
    * Caminho de recurso: Especifica o recurso ou a coleção de recursos, que pode incluir vários segmentos usados pelo serviço para determinar a seleção desses recursos. Por exemplo: `CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties` pode ser usado para obter as propriedades especificadas para o CatalogItem.
    * Cadeia de caracteres (opcional): fornece parâmetros adicionais de simples, como os critérios de seleção de recursos ou de versão de API.

* Campos de cabeçalho de mensagem de solicitação HTTP:

    * Necessário [método HTTP](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) (também conhecido como uma operação ou verbo), que informa o serviço que tipo de operação que você está solicitando. Relatórios que APIs REST de serviços de suporte à exclusão, GET, HEAD, PUT, POST e métodos do PATCH.
    * Campos de cabeçalho adicionais opcionais, conforme exigido pelo método HTTP e o URI especificado.

* HTTP opcional **corpo da mensagem de solicitação** campos, para dar suporte à operação de URI e HTTP. Por exemplo, operações de publicação contêm objetos codificado em MIME que são passados como parâmetros complexos. Para operações POST ou PUT, o tipo de codificação MIME para o corpo deve ser especificado no `Content-type` também o cabeçalho de solicitação. Alguns serviços exigem que você use um tipo MIME específico, como `application/json`.

* HTTP **cabeçalho da mensagem de resposta** campos:

    * Um [código de status HTTP](http://www.w3.org/Protocols/HTTP/HTRESP.html), intervalo de códigos de sucesso 2xx 4xx ou 5xx códigos de erro. Como alternativa, um código de status de serviço definido pode ser retornado, conforme indicado na documentação da API.
    * Campos de cabeçalho adicionais opcionais, conforme necessário para dar suporte a resposta da solicitação, como um `Content-type` cabeçalho de resposta.

* HTTP opcional **corpo da mensagem de resposta** campos:

    * Objetos de formato MIME de resposta são retornados no corpo da resposta HTTP, como uma resposta de um método GET que está retornando dados. Normalmente, esses objetos são retornados em um formato estruturado como JSON ou XML, conforme indicado pelo `Content-type` cabeçalho de resposta.

## <a name="api-documentation"></a>Documentação da API

Uma API REST modernos chamadas para documentação da API moderna. A API REST baseia-se na especificação OpenAPI (também conhecido como a especificação de swagger) e a documentação está disponível em [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0). Além da documentação da API, SwaggerHub ajuda a gerar uma biblioteca de cliente no idioma de preferência – JavaScript, TypeScript, c#, Java, Python, Ruby e muito mais.

## <a name="testing-api-calls"></a>Chamadas de API de teste

É uma ferramenta para testar as mensagens de solicitação/resposta HTTP [Fiddler](http://www.telerik.com/fiddler). O Fiddler é uma web gratuita proxy que pode interceptar solicitações REST, tornando mais fácil diagnosticar a solicitação HTTP de depuração / mensagens de resposta.

## <a name="next-steps"></a>Próximas etapas

Analisar as APIs disponíveis em [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0).

Os exemplos estão disponíveis em [GitHub](https://github.com/Microsoft/Reporting-Services). O exemplo inclui um aplicativo HTML5 baseado em TypeScript, reagir e webpack juntamente com um exemplo do PowerShell.

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
