---
title: Especificando um teste de nó no caminho do local (SQLXML 4.0) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d0a3dd41259bcbf2567d34a86527865de011faf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012673"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Especificando um teste de nó no caminho do local (SQLXML 4.0)
  Um teste de nó especifica o tipo de nó selecionado pela etapa de local. Todo eixo (`child`, `parent`, `attribute` ou `self`) tem um tipo de nó principal. Para o `attribute` eixo, o tipo de nó principal é  **\<atributo >** . Para o `parent`, `child`, e `self` eixos, o tipo de nó principal é  **\<elemento >** .  
  
> [!NOTE]  
>  O teste de nó de curinga * (por exemplo, `child::*`) não tem suporte.  
  
## <a name="node-test-example-1"></a>Teste de nó: Exemplo 1  
 O caminho do local `child::Customer` seleciona  **\<cliente >** elementos filhos do nó de contexto.  
  
 Neste exemplo, `child` é o eixo e `Customer` é o teste de nó. O tipo de nó principal para o `child` eixo é  **\<elemento >** . Portanto, o teste de nó será TRUE se o  **\<cliente >** nó for um  **\<elemento >** nó. Se o nó de contexto não tiver nenhuma  **\<cliente >** filhos, um conjunto de nós vazio será retornado.  
  
## <a name="node-test-example-2"></a>Teste de nó: Exemplo 2  
 O caminho do local `attribute::CustomerID` seleciona o **CustomerID** atributo do nó de contexto.  
  
 No exemplo, `attribute` é o eixo e `CustomerID` é o teste de nó. O tipo de nó principal do `attribute` eixo é  **\<atributo >** . Portanto, o teste de nó será TRUE se **CustomerID** é um  **\<atributo >** nó. Se o nó de contexto não tiver nenhuma **CustomerID**, um conjunto de nós vazio será retornado.  
  
> [!NOTE]  
>  Nessa implementação de XPath, se uma etapa de local se refere a um  **\<elemento >** ou uma  **\<atributo >** tipo que não está declarado no esquema, um erro será gerado. Isto é diferente da implementação de XPath em MSXML, que retorna um conjunto de nós vazio.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintaxe abreviada para os eixos  
 A sintaxe abreviada a seguir para o caminho de local tem suporte:  
  
-   `attribute::` pode ser abreviado para `@`.  
  
     O caminho do local `Customer[@CustomerID="ALFKI"]` é o mesmo que `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` pode ser omitido de uma etapa de local.  
  
     Assim, `child` é o eixo padrão. O caminho do local `Customer/Order` é o mesmo que `child::Customer/child::Order`.  
  
-   `self::node()` pode ser abreviado como um ponto (.) e `parent::node()` pode ser abreviado como dois pontos (..).  
  
  
