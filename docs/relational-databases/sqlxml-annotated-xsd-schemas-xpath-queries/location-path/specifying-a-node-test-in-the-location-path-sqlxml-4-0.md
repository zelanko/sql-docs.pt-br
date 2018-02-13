---
title: "Especificando um teste de nó no caminho do local (SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e7e2483b8bf861a677e1fbe7b417376bb266e7f4
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Especificando um teste de nó no caminho do local (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Um teste de nó especifica o tipo de nó selecionado pela etapa de local. Cada eixo (**filho**, **pai**, **atributo**, ou **self**) tem um tipo de nó principal. Para o **atributo** eixo, o tipo de nó principal é  **\<atributo >**. Para o **pai**, **filho**, e **self** eixos, o tipo de nó principal é  **\<elemento >**.  
  
> [!NOTE]  
>  O teste de nó de curinga * (por exemplo, `child::*`) não tem suporte.  
  
## <a name="node-test-example-1"></a>Teste de nó: Exemplo 1  
 O caminho do local `child::Customer` seleciona  **\<cliente >** elementos filhos do nó de contexto.  
  
 Neste exemplo, `child` é o eixo e `Customer` é o teste de nó. O tipo de nó principal para o **filho** eixo é  **\<elemento >**. Portanto, o teste de nó será TRUE se o  **\<cliente >** nó é um  **\<elemento >** nó. Se o nó de contexto não tiver nenhuma  **\<cliente >** filhos, um conjunto de nós vazio será retornado.  
  
## <a name="node-test-example-2"></a>Teste de nó: exemplo 2  
 O caminho do local `attribute::CustomerID` seleciona o **CustomerID** atributo do nó de contexto.  
  
 No exemplo, `attribute` é o eixo e `CustomerID` é o teste de nó. O tipo de nó principal do **atributo** eixo é  **\<atributo >**. Portanto, o teste de nó será TRUE se **CustomerID** é um  **\<atributo >** nó. Se o nó de contexto não tiver nenhuma **CustomerID**, um conjunto de nós vazio será retornado.  
  
> [!NOTE]  
>  Nessa implementação do XPath, se uma etapa de local refere-se a uma  **\<elemento >** ou um  **\<atributo >** tipo que não está declarado no esquema, será gerado um erro. Isto é diferente da implementação de XPath em MSXML, que retorna um conjunto de nós vazio.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Sintaxe abreviada para os eixos  
 A sintaxe abreviada a seguir para o caminho de local tem suporte:  
  
-   `attribute::` pode ser abreviado para `@`.  
  
     O caminho do local `Customer[@CustomerID="ALFKI"]` é o mesmo que `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` pode ser omitido de uma etapa de local.  
  
     Portanto, **filho** é o eixo padrão. O caminho do local `Customer/Order` é o mesmo que `child::Customer/child::Order`.  
  
-   `self::node()` pode ser abreviado como um ponto (.) e `parent::node()` pode ser abreviado como dois pontos (..).  
  
  
