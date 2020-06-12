---
title: Definir predicados de seleção no caminho do local (SQLXML)
description: Saiba como a especificação de predicados de seleção na expressão de caminho de local de uma consulta XPath (SQLXML 4,0) filtra o conjunto de nós que está sendo consultado.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3f62aa328573011d61a4a650aeb117516c3f9a6
ms.sourcegitcommit: 6593b3b6365283bb76c31102743cdccc175622fe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84306180"
---
# <a name="specifying-selection-predicates-in-the-location-path-sqlxml-40"></a>Especificando predicados de seleção no caminho do local (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um predicado filtra um conjunto de nós com respeito a um eixo (semelhantemente a uma cláusula WHERE em uma instrução SELECT). O predicado é especificado entre colchetes. Para cada nó no conjunto de nós a ser filtrado, a expressão de predicado é avaliada com esse nó como o nó de contexto, com o número de nós no conjunto de nós como o tamanho do contexto. Se a expressão de predicado for avaliada como TRUE para esse nó, o nó será incluído no conjunto de nós resultante.  
  
 XPath também permite a filtragem com base na posição. Uma expressão de predicado avaliada como um número seleciona esse nó ordinal. Por exemplo, o caminho do local `Customer[3]` retorna o terceiro cliente. Não há suporte para tais predicados numéricos. Há suporte somente para expressões de predicado que retornem um resultado Boolean.  
  
> [!NOTE]  
>  Para obter informações sobre as limitações dessa implementação XPath do XPath e as diferenças entre ela e a especificação W3C, consulte [introdução ao uso de consultas XPath &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/introduction-to-using-xpath-queries-sqlxml-4-0.md).  
  
## <a name="selection-predicate-example-1"></a>Predicado de seleção: exemplo 1  
 A seguinte expressão XPath (caminho do local) seleciona a partir do nó de contexto atual todos os **\<Customer>** filhos do elemento que têm o atributo **CustomerID** com o valor de ALFKI:  
  
```  
/child::Customer[attribute::CustomerID="ALFKI"]  
```  
  
 Nesta consulta XPath, `child` e `attribute` são nomes de eixo. `Customer`é o teste de nó (verdadeiro se `Customer` for um **\<element node>** , porque **\<element>** é o tipo de nó principal para o `child` eixo). `attribute::CustomerID="ALFKI"` é o predicado. No predicado, `attribute` é o eixo e `CustomerID` é o teste de nó (true se **CustomerID** é um atributo do nó de contexto, porque **\<attribute>** é o tipo de nó principal do eixo de **atributo** ).  
  
 Usando a sintaxe abreviada, a consulta XPath também pode ser especificada como:  
  
```  
/Customer[@CustomerID="ALFKI"]  
```  
  
## <a name="selection-predicate-example-2"></a>Predicado de seleção: exemplo 2  
 A seguinte expressão XPath (caminho de localização) seleciona a partir do nó de contexto atual todos os **\<Order>** netos que têm o atributo **SalesOrderID** com o valor 1:  
  
```  
/child::Customer/child::Order[attribute::SalesOrderID="1"]  
```  
  
 Nesta expressão XPath, `child` e `attribute` são os nomes de eixo. `Customer`, `Order` e `SalesOrderID` são os testes de nó. `attribute::OrderID="1"` é o predicado.  
  
 Usando a sintaxe abreviada, a consulta XPath também pode ser especificada como:  
  
```  
/Customer/Order[@SalesOrderID="1"]  
```  
  
## <a name="selection-predicate-example-3"></a>Predicado de seleção: exemplo 3  
 A seguinte expressão XPath (caminho de localização) seleciona a partir do nó de contexto atual todos os **\<Customer>** filhos que têm um ou mais **\<ContactName>** filhos:  
  
```  
child::Customer[child::ContactName]  
```  
  
 Este exemplo pressupõe que o **\<ContactName>** é um elemento filho do **\<Customer>** elemento no documento XML, que é conhecido como *mapeamento centrado em elemento* em um esquema XSD anotado.  
  
 Nesta expressão XPath, `child` é o nome do eixo. `Customer`é o teste de nó (TRUE se `Customer` for um **\<element>** nó, porque **\<element>** é o tipo de nó principal para `child` Axis). `child::ContactName` é o predicado. No predicado, `child` é o eixo e `ContactName` é o teste de nó (verdadeiro se `ContactName` for um **\<element>** nó).  
  
 Essa expressão retorna somente os **\<Customer>** filhos do elemento do nó de contexto que têm **\<ContactName>** elementos filhos.  
  
 Usando a sintaxe abreviada, a consulta XPath também pode ser especificada como:  
  
```  
Customer[ContactName]  
```  
  
## <a name="selection-predicate-example-4"></a>Predicado de seleção: exemplo 4  
 A expressão XPath a seguir seleciona **\<Customer>** elementos filhos do nó de contexto que não têm **\<ContactName>** elementos filho:  
  
```  
child::Customer[not(child::ContactName)]  
```  
  
 Este exemplo pressupõe que **\<ContactName>** é um elemento filho do **\<Customer>** elemento no documento XML, e o campo ContactName não é necessário no banco de dados.  
  
 Neste exemplo, `child` é o eixo. `Customer`é o teste de nó (verdadeiro se `Customer` for um \<element> nó). `not(child::ContactName)` é o predicado. No predicado, `child` é o eixo e `ContactName` é o teste de nó (verdadeiro se `ContactName` for um \<element> nó).  
  
 Usando a sintaxe abreviada, a consulta XPath também pode ser especificada como:  
  
```  
Customer[not(ContactName)]  
```  
  
## <a name="selection-predicate-example-5"></a>Predicado de seleção: exemplo 5  
 A expressão XPath a seguir seleciona a partir do nó de contexto atual todos os **\<Customer>** filhos que têm o atributo **CustomerID** :  
  
```  
child::Customer[attribute::CustomerID]  
```  
  
 Neste exemplo, `child` é o eixo e `Customer` é o teste de nó (verdadeiro se `Customer` for um \<element> nó). `attribute::CustomerID` é o predicado. No predicado, `attribute` é o eixo e `CustomerID` é o predicado (true se `CustomerID` for um **\<attribute>** nó).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Introdução aos esquemas XSD anotados &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)   
 [Formatação XML do lado do cliente &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)  
  
  
