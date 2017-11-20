---
title: "Junções externas | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aff4448df5ec42e29da6c49fe0ace7f0334a1174
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="outer-joins"></a>Junções externas
ODBC oferece suporte a SQL-92 à esquerda, sintaxe de junção externa completa e à direita. É a sequência de escape de junções externas  
  
 **{oj** *junção externa***}**  
  
 onde *junção externa* é  
  
 *referência de tabela* {**esquerda &#124; DIREITA &#124; JUNÇÃO externa completa}** {*referência de tabela* &#124; *junção externa*} **ON** *critério de pesquisa*  
  
 *referência de tabela* Especifica um nome de tabela e *critério de pesquisa* Especifica a condição de junção entre a *referências de tabela*.  
  
 Uma solicitação de junção externa deve aparecer após o **FROM** palavra-chave e antes do **onde** cláusula (se houver). Para obter informações de sintaxe completa, consulte [Outer Join sequência de Escape](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) na gramática do apêndice c: SQL.  
  
 Por exemplo, as seguintes instruções SQL criam o mesmo conjunto de resultados que lista todos os clientes e mostra o que tem pedidos pendentes. A primeira instrução usa a sintaxe de sequência de escape. A segunda instrução usa a sintaxe de nativo para Oracle e não é interoperável.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Para determinar os tipos de junções externas que dão suporte a uma fonte de dados e o driver, um aplicativo chama **SQLGetInfo** com o SQL_OJ_CAPABILITIES flag. Os tipos de junções externas que podem ter suporte são esquerdos, direita, completo ou junções externas; aninhadas junções externas no qual os nomes de coluna no **ON** cláusula não tem a mesma ordem que seus nomes de tabela do respectivos no **OUTER JOIN** cláusula; junções internas em conjunto com junções externas; e junções externas usando qualquer operador de comparação ODBC. Se o tipo de informação SQL_OJ_CAPABILITIES retorna 0, não há suporte para nenhuma cláusula de junção externa.

