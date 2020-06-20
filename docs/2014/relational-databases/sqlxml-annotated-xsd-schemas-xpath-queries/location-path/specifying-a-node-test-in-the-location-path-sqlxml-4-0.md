---
title: Especificando um teste de nó no caminho do local (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
author: rothja
ms.author: jroth
ms.openlocfilehash: 02f78577eab391f1774251ad2c6ca7b9a4bd2dab
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85015224"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Especificando um teste de nó no caminho do local (SQLXML 4.0)
  Um teste de nó especifica o tipo de nó selecionado pela etapa de local. Todo eixo (`child`, `parent`, `attribute` ou `self`) tem um tipo de nó principal. Para o `attribute` eixo, o tipo de nó principal é **\<attribute>** . Para os `parent` `child` eixos,, e `self` , o tipo de nó principal é **\<element>** .  
  
> [!NOTE]  
>  O teste de nó de curinga * (por exemplo, `child::*`) não tem suporte.  
  
## <a name="node-test-example-1"></a>Teste de nó: exemplo 1  
 O caminho do local `child::Customer` seleciona os **\<Customer>** filhos do elemento do nó de contexto.  
  
 Neste exemplo, `child` é o eixo e `Customer` é o teste de nó. O tipo de nó de entidade para o `child` eixo é **\<element>** . Portanto, o teste de nó será TRUE se o **\<Customer>** nó for um **\<element>** nó. Se o nó de contexto não tiver **\<Customer>** filhos, um conjunto de nós vazio será retornado.  
  
## <a name="node-test-example-2"></a>Teste de nó: exemplo 2  
 O caminho do local `attribute::CustomerID` seleciona o atributo **CustomerID** do nó de contexto.  
  
 No exemplo, `attribute` é o eixo e `CustomerID` é o teste de nó. O tipo de nó principal do `attribute` eixo é **\<attribute>** . Portanto, o teste de nó será TRUE se **CustomerID** for um **\<attribute>** nó. Se o nó de contexto não tiver nenhum **CustomerID**, um conjunto de nós vazio será retornado.  
  
> [!NOTE]  
>  Nessa implementação do XPath, se uma etapa de local se refere a um **\<element>** ou um **\<attribute>** tipo que não está declarado no esquema, um erro é gerado. Isto é diferente da implementação de XPath em MSXML, que retorna um conjunto de nós vazio.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintaxe abreviada para os eixos  
 A sintaxe abreviada a seguir para o caminho de local tem suporte:  
  
-   `attribute::` pode ser abreviado para `@`.  
  
     O caminho do local `Customer[@CustomerID="ALFKI"]` é o mesmo que `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` pode ser omitido de uma etapa de local.  
  
     Assim, `child` é o eixo padrão. O caminho do local `Customer/Order` é o mesmo que `child::Customer/child::Order`.  
  
-   `self::node()` pode ser abreviado como um ponto (.) e `parent::node()` pode ser abreviado como dois pontos (..).  
  
  
