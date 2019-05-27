---
title: Especificando predicados de seleção no caminho do local (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], predicates
- predicates [SQLXML]
- position-based filtering [SQLXML]
- XPath queries [SQLXML], location paths
- filtering [SQLXML]
- location path for XPath query
ms.assetid: dbef4cf4-a89b-4d7e-b72b-4062f7b29a80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d35b70c157dc5285355fcd15b38739757f0be9a
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012578"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>Especificando predicados de seleção no caminho do local (SQLXML 4.0)
  Um predicado filtra um conjunto de nós com respeito a um eixo (semelhantemente a uma cláusula WHERE em uma instrução SELECT). O predicado é especificado entre colchetes. Para cada nó no conjunto de nós a ser filtrado, a expressão de predicado é avaliada com esse nó como o nó de contexto, com o número de nós no conjunto de nós como o tamanho do contexto. Se a expressão de predicado for avaliada como TRUE para esse nó, o nó será incluído no conjunto de nós resultante.  
  
 XPath também permite a filtragem com base na posição. Uma expressão de predicado avaliada como um número seleciona esse nó ordinal. Por exemplo, o caminho do local `Customer[3]` retorna o terceiro cliente. Não há suporte para tais predicados numéricos. Há suporte somente para expressões de predicado que retornem um resultado Boolean.  
  
> [!NOTE]  
>  Para obter informações sobre as limitações desta implementação XPath do XPath e as diferenças entre ele e a especificação do W3C, consulte [Introdução a consultas de XPath usando &#40;SQLXML 4.0&#41;](../introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="selection-predicate-example-1"></a>Predicado de seleção: Exemplo 1  
 A seguinte expressão XPath (caminho do local) seleciona do nó de contexto atual todos os as  **\<cliente >** filhos do elemento que tem o **CustomerID** atributo com valor ALFKI:  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 Nesta consulta XPath, `child` e `attribute` são nomes de eixo. `Customer` é o teste de nó (TRUE se `Customer` é um  **\<nó de elemento >**, pois  **\<elemento >** é o tipo de nó principal para o `child` eixo). `attribute::CustomerID="ALFKI"` é o predicado. No predicado, `attribute` é o eixo e `CustomerID` é o teste de nó (TRUE se **CustomerID** é um atributo do nó de contexto, pois  **\<atributo >** é a entidade de segurança tipo de nó `attribute` eixo).  
  
 Usando a sintaxe abreviada, a consulta XPath também pode ser especificada como:  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>Predicado de seleção: Exemplo 2  
 A seguinte expressão XPath (caminho do local) seleciona do nó de contexto atual todos os as  **\<ordem >** netos do elemento que tem o **SalesOrderID** atributo com o valor 1:  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 Nesta expressão XPath, `child` e `attribute` são os nomes de eixo. `Customer`, `Order` e `SalesOrderID` são os testes de nó. `attribute::OrderID="1"` é o predicado.  
  
 Usando a sintaxe abreviada, a consulta XPath também pode ser especificada como:  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>Predicado de seleção: Exemplo 3  
 A seguinte expressão XPath (caminho do local) seleciona do nó de contexto atual todos os  **\<cliente >** filhos que têm uma ou mais  **\<ContactName >** filhos:  
  
```  
child::Customer[child::ContactName]  
```  
  
 Este exemplo supõe que o  **\<ContactName >** é um elemento filho do  **\<cliente >** elemento no documento XML, que é conhecido como  *mapeamento centrado em elemento* em um esquema XSD anotado.  
  
 Nesta expressão XPath, `child` é o nome do eixo. `Customer` é o teste de nó (TRUE se `Customer` é um  **\<elemento >** nó, pois  **\<elemento >** é o tipo de nó principal para `child` eixo). `child::ContactName` é o predicado. O predicado `child` é o eixo e `ContactName` é o teste de nó (TRUE se `ContactName` é um  **\<elemento >** nó).  
  
 Essa expressão retorna somente o  **\<cliente >** filhos do elemento do nó de contexto que tenham  **\<ContactName >** filhos do elemento.  
  
 Usando a sintaxe abreviada, a consulta XPath também pode ser especificada como:  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>Predicado de seleção: Exemplo 4  
 A seguinte expressão XPath seleciona  **\<cliente >** filhos do elemento do nó de contexto que não têm  **\<ContactName >** filhos do elemento:  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 Este exemplo supõe que  **\<ContactName >** é um elemento filho do  **\<cliente >** elemento no documento XML e o campo ContactName não é necessário o banco de dados.  
  
 Neste exemplo, `child` é o eixo. `Customer` é o teste de nó (TRUE se `Customer` é um \<elemento > nó). `not(child::ContactName)` é o predicado. O predicado `child` é o eixo e `ContactName` é o teste de nó (TRUE se `ContactName` é um \<elemento > nó).  
  
 Usando a sintaxe abreviada, a consulta XPath também pode ser especificada como:  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>Predicado de seleção: Exemplo 5  
 A seguinte expressão XPath seleciona do nó de contexto atual todos os  **\<cliente >** filhos que têm o **CustomerID** atributo:  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 Neste exemplo, `child` é o eixo e `Customer` é o teste de nó (TRUE se `Customer` é um \<elemento > nó). `attribute::CustomerID` é o predicado. O predicado `attribute` é o eixo e `CustomerID` é o predicado (TRUE se `CustomerID` é um  **\<atributo >** nó).  
  
 Usando a sintaxe abreviada, a consulta XPath também pode ser especificada como:  
  
```  
Customer[@CustomerID]  
```  
  
## <a name="selection-predicate-example-6"></a>Predicado de seleção: Exemplo 6  
 O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 inclui suporte para consultas XPath que contenham um produto cruzado no predicado, conforme mostrado no seguinte exemplo:  
  
```  
Customer[Order/@OrderDate=Order/@ShipDate]  
```  
  
 Esta consulta seleciona todos os clientes com qualquer `Order` para o qual `OrderDate` é igual a qualquer `ShipDate` de qualquer `Order`.  
  
## <a name="see-also"></a>Consulte também  
 [Introdução a esquemas XSD anotados &#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [Formatação XML do lado do cliente &#40;SQLXML 4.0&#41;](../../sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
