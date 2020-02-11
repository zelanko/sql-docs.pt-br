---
title: Especificando um eixo (SQLXML)
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a219c2093832b979171584d5559da359b574552e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75253061"
---
# <a name="specifying-an-axis-sqlxml-40"></a>Especificando um eixo (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
-   O eixo especifica a relação de árvore entre os nós selecionados pela etapa de local e o nó de contexto. Há suporte para os seguintes eixos: **filho**  
  
     Contém o filho do nó de contexto.  
  
     A seguinte expressão XPath (caminho de localização) seleciona no nó de contexto atual todos os>filhos do ** \<cliente** :  
  
    ```  
    child::Customer  
    ```  
  
     Na consulta XPath a seguir, `child` é o eixo. 
  `Customer` é o teste de nó.  
  
-   **primária**  
  
     Contém o pai do nó de contexto.  
  
     A expressão XPath a seguir seleciona todos os ** \<clientes>** pais da ** \<ordem>** filhos:  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     Isso corresponde à especificação de `child::Customer`. Nesta consulta XPath, `child` e `parent` são os eixos. 
  `Customer` e `Order` são os testes de nó.  
  
-   **Attribute**  
  
     Contém o atributo do nó de contexto.  
  
     A expressão XPath a seguir seleciona o atributo **CustomerID** do nó de contexto:  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **auto-restauração**  
  
     Contém o próprio nó de contexto.  
  
     A expressão XPath a seguir selecionará o nó atual se for o nó de ** \<>de ordem** :  
  
    ```  
    self::Order  
    ```  
  
     Nesta consulta XPath, `self` é o eixo e `Order` é o teste de nó.  
  
  
