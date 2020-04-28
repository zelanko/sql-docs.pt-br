---
title: Especificando um teste de nó no caminho do local (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f94f155ee86df6daf0c039a18f27c30e294d57df
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75254744"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Especificando um teste de nó no caminho do local (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um teste de nó especifica o tipo de nó selecionado pela etapa de local. Cada eixo (**filho**, **pai**, **atributo**ou **próprio**) tem um tipo de nó principal. Para o eixo de **atributo** , o tipo de nó principal é ** \<>de atributo **. Para os eixos **pai**, **filho**e **Self** , o tipo de nó principal é ** \<>de elemento **.  
  
> [!NOTE]  
>  O teste de nó de curinga * (por exemplo, `child::*`) não tem suporte.  
  
## <a name="node-test-example-1"></a>Teste de nó: exemplo 1  
 O caminho `child::Customer` do local seleciona ** \<** os filhos do elemento de>do cliente do nó de contexto.  
  
 Neste exemplo, `child` é o eixo e `Customer` é o teste de nó. O tipo de nó de entidade para o eixo **filho** é ** \<>de elemento **. Portanto, o teste de nó será verdadeiro se o nó do ** \<cliente>** for um ** \<elemento>** nó. Se o nó de contexto não tiver nenhum ** \<cliente>** filhos, um conjunto vazio de nós será retornado.  
  
## <a name="node-test-example-2"></a>Teste de nó: exemplo 2  
 O caminho `attribute::CustomerID` do local seleciona o atributo **CustomerID** do nó de contexto.  
  
 No exemplo, `attribute` é o eixo e `CustomerID` é o teste de nó. O tipo de nó principal do eixo de **atributo** é ** \<o atributo>**. Portanto, o teste de nó será true se **CustomerID** for um ** \<atributo>** nó. Se o nó de contexto não tiver nenhum **CustomerID**, um conjunto de nós vazio será retornado.  
  
> [!NOTE]  
>  Nessa implementação do XPath, se uma etapa de local se refere a um ** \<elemento>** ou um ** \<** tipo de>de atributo que não é declarado no esquema, um erro é gerado. Isto é diferente da implementação de XPath em MSXML, que retorna um conjunto de nós vazio.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintaxe abreviada para os eixos  
 A sintaxe abreviada a seguir para o caminho de local tem suporte:  
  
-   `attribute::` pode ser abreviado para `@`.  
  
     O caminho do local `Customer[@CustomerID="ALFKI"]` é o mesmo que `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` pode ser omitido de uma etapa de local.  
  
     Portanto, **Child** é o eixo padrão. O caminho do local `Customer/Order` é o mesmo que `child::Customer/child::Order`.  
  
-   `self::node()` pode ser abreviado como um ponto (.) e `parent::node()` pode ser abreviado como dois pontos (..).  
  
  
