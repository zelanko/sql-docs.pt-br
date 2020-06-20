---
title: Especificando um eixo (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- XPath queries [SQLXML], location paths
- self axis
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- location path for XPath query
- axes [SQLXML]
ms.assetid: 65631795-3389-40cf-90ea-85e9438956c5
author: rothja
ms.author: jroth
ms.openlocfilehash: 651b7899e104fe5a7dbc6d584ceba6e5cf8de570
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055119"
---
# <a name="specifying-an-axis-sqlxml-40"></a>Especificando um eixo (SQLXML 4.0)
    
-   O eixo especifica a relação de árvore entre os nós selecionados pela etapa de local e o nó de contexto. Há suporte para os seguintes eixos: `child`  
  
     Contém o filho do nó de contexto.  
  
     A seguinte expressão XPath (caminho de localização) seleciona a partir do nó de contexto atual todos os **\<Customer>** filhos:  
  
    ```  
    child::Customer  
    ```  
  
     Na consulta XPath a seguir, `child` é o eixo. `Customer` é o teste de nó.  
  
-   `parent`  
  
     Contém o pai do nó de contexto.  
  
     A expressão XPath a seguir seleciona todos os **\<Customer>** pais dos **\<Order>** filhos:  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     Isso corresponde à especificação de `child::Customer`. Nesta consulta XPath, `child` e `parent` são os eixos. `Customer` e `Order` são os testes de nó.  
  
-   `attribute`  
  
     Contém o atributo do nó de contexto.  
  
     A expressão XPath a seguir seleciona o atributo **CustomerID** do nó de contexto:  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   `self`  
  
     Contém o próprio nó de contexto.  
  
     A expressão XPath a seguir selecionará o nó atual se ele for o **\<Order>** nó:  
  
    ```  
    self::Order  
    ```  
  
     Nesta consulta XPath, `self` é o eixo e `Order` é o teste de nó.  
  
  
