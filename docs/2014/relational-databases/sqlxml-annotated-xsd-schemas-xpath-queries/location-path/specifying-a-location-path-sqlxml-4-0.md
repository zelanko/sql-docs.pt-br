---
title: Especificando um caminho de local (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- absolute location path
- node-set [SQLXML]
- XPath queries [SQLXML], location paths
- relative location path [SQLXML]
- location path for XPath query
ms.assetid: a23a2b75-bc69-49f0-99db-05e14dc15bc0
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 86ff805cb06248cb0348d44b137affa3b4563444
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286893"
---
# <a name="specifying-a-location-path-sqlxml-40"></a>Especificando um caminho para o local (SQLXML 4.0)
  São especificadas consultas XPath no formato de uma expressão. Há vários tipos de expressões. Um caminho de local é uma expressão que seleciona um conjunto de nós relativos ao nó de contexto. O resultado de avaliar um caminho de local é um conjunto de nós.  
  
## <a name="types-of-location-paths"></a>Tipos de caminhos de local  
 Um caminho de local pode ter um destes formatos:  
  
-   **Caminho de local absoluto**  
  
     Um caminho de local absoluto inicia no nó raiz do documento. Ele é formado por barra (/) opcionalmente seguida por um caminho de local relativo. A barra (/) seleciona o nó raiz do documento.  
  
-   **Caminho de local relativo**  
  
     Um caminho de local relativo inicia no nó de contexto no documento. Um caminho de local consiste em uma sequência de uma ou mais etapas de local separada por uma barra (/). Cada etapa seleciona um conjunto de nós relativo ao nó de contexto. A sequência inicial de etapas seleciona um conjunto de nós relativo a um nó de contexto. Cada nó nesse conjunto é usado como um nó de contexto para a etapa seguinte. São unidos os conjuntos de nós identificados por esta etapa. Por exemplo, **Child/child::OrderDetail** seleciona o  **\<OrderDetail >** filhos do elemento a  **\<ordem >** elemento filhos do nó de contexto.  
  
    > [!NOTE]  
    >  Na implementação de XPath do SQLXML 4.0, todas as consultas XPath começam no contexto raiz, mesmo que o XPath não seja explicitamente absoluto. Por exemplo, uma consulta XPath que comece com "Customer" é tratada como "/Customer". Na consulta XPath **Customer [Order]**, Customer começa no contexto raiz, mas Order começa no contexto de cliente. Para obter mais informações, consulte [Introdução a consultas de XPath usando &#40;SQLXML 4.0&#41;](../introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="location-steps"></a>Etapas de local  
 Um caminho de local (absoluto ou relativo) é composto por etapas de local que contêm três partes:  
  
-   **Axis**  
  
     O eixo especifica a relação de árvore entre os nós selecionados pela etapa de local e o nó de contexto. Os eixos `parent`, `child`, `attribute` e `self` são aceitos. Se um eixo `child` for especificado no caminho de local, todos os nós selecionados pela consulta serão os filhos do nó de contexto. Se um eixo `parent` for especificado, o nó selecionado será o nó pai do nó de contexto. Se um eixo `attribute` for especificado, os nós selecionados serão os atributos do nó de contexto.  
  
-   **Teste de nó**  
  
     Um teste de nó especifica o tipo de nó selecionado pela etapa de local. Todos os eixos (`child`, `parent`, `attribute` e `self`) têm um tipo de nó principal. Para o `attribute` eixo, o tipo de nó principal é  **\<atributo >**. Para o `parent`, `child`, e `self` eixos, o tipo de nó principal é  **\<elemento >**.  
  
     Por exemplo, se o caminho do local especifica **child::Customer**, o  **\<cliente >** elementos filhos do nó de contexto são selecionados. Porque o `child` eixo tiver  **\<elemento >** como seu tipo de nó principal, o teste de nó, o cliente, será TRUE se o cliente é um  **\<elemento >** nó.  
  
-   **Predicados de seleção (zero ou mais)**  
  
     Um predicado filtra um conjunto de nós em relação a um eixo. A especificação de predicados de seleção em uma expressão XPath é semelhante à especificação de uma cláusula WHERE em uma instrução SELECT. O predicado é especificado entre colchetes. A aplicação do teste especificado nos predicados de seleção filtra os nós retornados pelo teste de nó. Para cada nó no conjunto de nós a ser filtrado, a expressão de predicado é avaliada com esse nó como o nó de contexto, com o número de nós no conjunto de nós como o tamanho do contexto. Se a expressão de predicado for avaliada como TRUE para esse nó, o nó será incluído no conjunto de nós resultante.  
  
     A sintaxe de uma etapa de local é o nome do eixo e o teste de nó separados por dois-pontos duplos (::), seguidos por zero ou mais expressões entre colchetes. Por exemplo, a expressão XPath (caminho do local) **child::Customer [@CustomerID= 'ALFKI']** seleciona todos os  **\<cliente >** elementos filhos do nó de contexto. Em seguida, o teste no predicado é aplicado ao conjunto de nós, que retorna apenas o  **\<cliente >** nós de elemento com o atributo de valor 'ALFKI' para o seu **CustomerID** atributo.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Especificando um eixo &#40;SQLXML 4.0&#41;](specifying-an-axis-sqlxml-4-0.md)  
 Fornece exemplos de especificação de um eixo.  
  
 [Especificando um teste de nó no caminho do local &#40;SQLXML 4.0&#41;](specifying-a-node-test-in-the-location-path-sqlxml-4-0.md)  
 Fornece exemplos de especificação de um teste de nó.  
  
 [Especificando predicados de seleção no caminho do local &#40;SQLXML 4.0&#41;](specifying-selection-predicates-in-the-location-path-sqlxml-4-0.md)  
 Fornece exemplos de especificação de predicados de seleção.  
  
  
