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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8da239fd8a6bbf559f89ba5fd1b0fa0ab10ec190
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012644"
---
# <a name="specifying-an-axis-sqlxml-40"></a>Especificando um eixo (SQLXML 4.0)
    
-   O eixo especifica a relação de árvore entre os nós selecionados pela etapa de local e o nó de contexto. Há suporte para os seguintes eixos: `child`  
  
     Contém o filho do nó de contexto.  
  
     A seguinte expressão XPath (caminho de localização) seleciona no nó de contexto atual todos os>filhos do ** \<cliente** :  
  
    ```  
    child::Customer  
    ```  
  
     Na consulta XPath a seguir, `child` é o eixo. 
  `Customer` é o teste de nó.  
  
-   `parent`  
  
     Contém o pai do nó de contexto.  
  
     A expressão XPath a seguir seleciona todos os ** \<clientes>** pais da ** \<ordem>** filhos:  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     Isso corresponde à especificação de `child::Customer`. Nesta consulta XPath, `child` e `parent` são os eixos. 
  `Customer` e `Order` são os testes de nó.  
  
-   `attribute`  
  
     Contém o atributo do nó de contexto.  
  
     A expressão XPath a seguir seleciona o atributo **CustomerID** do nó de contexto:  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   `self`  
  
     Contém o próprio nó de contexto.  
  
     A expressão XPath a seguir selecionará o nó atual se for o nó de ** \<>de ordem** :  
  
    ```  
    self::Order  
    ```  
  
     Nesta consulta XPath, `self` é o eixo e `Order` é o teste de nó.  
  
  
