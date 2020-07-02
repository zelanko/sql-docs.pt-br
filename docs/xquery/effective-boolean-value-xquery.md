---
title: Valor booliano efetivo (XQuery) | Microsoft Docs
description: Saiba mais sobre valores Boolianos efetivos no XQuery.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- Boolean values
- XQuery, effective Boolean values
- EBV
ms.assetid: 506682b1-b6c9-45e2-aa54-7abd5844c3f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 748042147b2e776c096296a98ce27dbc645e2d49
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753653"
---
# <a name="effective-boolean-value-xquery"></a>Valor Booliano efetivo (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Estes são os valores  Boolianos efetivos:  
  
-   False se o operando for uma sequência vazia ou um booliano false.  
  
-   Caso contrário, o valor é true.  
  
 O valor Booliano efetivo pode ser calculado para expressões que retornem um único valor Booliano, uma sequência de nó ou uma sequência vazia. Observe que o valor Booliano é calculado implicitamente quando os seguintes tipos de expressões são processados:  
  
-   Expressões lógicas  
  
-   A [função not](../xquery/functions-on-boolean-values-not-function.md)  
  
-   A cláusula WHERE de uma expressão FLWOR  
  
-   [Expressões condicionais](../xquery/conditional-expressions-xquery.md)  
  
-   [Expressões quantificadas](../xquery/quantified-expressions-xquery.md)  
  
 A seguir é apresentado um exemplo de valor Booliano efetivo. Quando a expressão **If** é processada, o valor booliano efetivo da condição é determinado. Como `/a[1]` retorna uma sequência vazia, o valor Booliano efetivo é false. O resultado é retornado como XML com um nó de texto (false).  
  
```  
value is false  
DECLARE @x XML  
SET @x = '<b/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 No exemplo a seguir, o valor Booliano efetivo é true, pois a expressão retorna uma sequência não vazia.  
  
```  
DECLARE @x XML  
SET @x = '<a/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 Ao consultar colunas ou variáveis **XML** tipadas, você pode ter nós do tipo booliano. Os **dados ()** , nesse caso, retorna um valor booliano. Se a expressão de consulta retorna um valor Booliano true, o valor Booliano efetivo é true, como exibido no exemplo a seguir. O exemplo também ilustra o seguinte:  
  
-   Uma coleção de esquemas XML é criada. O elemento \<b> na coleção é do tipo booliano.  
  
-   Uma variável **XML** com tipo é criada e consultada.  
  
-   A expressão `data(/b[1])` retorna um valor Booliano true. Portanto, o valor Booliano efetivo nesse caso, é true.  
  
-   A expressão `data(/b[2])` retorna um valor falso booliano. Portanto, o valor Booliano efetivo nesse caso, é false.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="s" type="string"/>  
      <element name="b" type="boolean"/>  
</schema>'  
go  
DECLARE @x XML(SC)  
SET @x = '<b>true</b><b>false</b>'  
SELECT @x.query('if (data(/b[1])) then "true" else "false"')  
SELECT @x.query('if (data(/b[2])) then "true" else "false"')  
go  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas do XQuery](../xquery/xquery-basics.md)   
 [Instrução FLWOR e iteração &#40;XQuery&#41;](../xquery/flwor-statement-and-iteration-xquery.md)  
  
  
