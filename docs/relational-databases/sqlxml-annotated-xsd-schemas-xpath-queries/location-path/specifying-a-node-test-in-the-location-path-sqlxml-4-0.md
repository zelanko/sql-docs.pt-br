---
title: Especificando um teste de nó no caminho do local (SQLXML)
description: Saiba como especificar um teste de nó no caminho do local de uma consulta XPath 4,0 do SQLXML.
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
ms.openlocfilehash: e0b7934b73589f71e5152bff33b2080c6eeb353e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85649743"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Especificando um teste de nó no caminho do local (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Um teste de nó especifica o tipo de nó selecionado pela etapa de local. Cada eixo (**filho**, **pai**, **atributo**ou **próprio**) tem um tipo de nó principal. Para o eixo de **atributo** , o tipo de nó principal é **\<attribute>** . Para os eixos **pai**, **filho**e **Self** , o tipo de nó principal é **\<element>** .  
  
> [!NOTE]  
>  O teste de nó de curinga * (por exemplo, `child::*`) não tem suporte.  
  
## <a name="node-test-example-1"></a>Teste de nó: exemplo 1  
 O caminho do local `child::Customer` seleciona os **\<Customer>** filhos do elemento do nó de contexto.  
  
 Neste exemplo, `child` é o eixo e `Customer` é o teste de nó. O tipo de nó de entidade para o eixo **filho** é **\<element>** . Portanto, o teste de nó será TRUE se o **\<Customer>** nó for um **\<element>** nó. Se o nó de contexto não tiver **\<Customer>** filhos, um conjunto de nós vazio será retornado.  
  
## <a name="node-test-example-2"></a>Teste de nó: exemplo 2  
 O caminho do local `attribute::CustomerID` seleciona o atributo **CustomerID** do nó de contexto.  
  
 No exemplo, `attribute` é o eixo e `CustomerID` é o teste de nó. O tipo de nó principal do eixo de **atributo** é **\<attribute>** . Portanto, o teste de nó será TRUE se **CustomerID** for um **\<attribute>** nó. Se o nó de contexto não tiver nenhum **CustomerID**, um conjunto de nós vazio será retornado.  
  
> [!NOTE]  
>  Nessa implementação do XPath, se uma etapa de local se refere a um **\<element>** ou um **\<attribute>** tipo que não está declarado no esquema, um erro é gerado. Isto é diferente da implementação de XPath em MSXML, que retorna um conjunto de nós vazio.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintaxe abreviada para os eixos  
 A sintaxe abreviada a seguir para o caminho de local tem suporte:  
  
-   `attribute::` pode ser abreviado para `@`.  
  
     O caminho do local `Customer[@CustomerID="ALFKI"]` é o mesmo que `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` pode ser omitido de uma etapa de local.  
  
     Portanto, **Child** é o eixo padrão. O caminho do local `Customer/Order` é o mesmo que `child::Customer/child::Order`.  
  
-   `self::node()` pode ser abreviado como um ponto (.) e `parent::node()` pode ser abreviado como dois pontos (..).  
  
  
