---
title: Junções externas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35f1ce877d6ed8a390bb6425a4d7f33a5d6947d2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513988"
---
# <a name="outer-joins"></a>Junções externas
ODBC dá suporte a SQL-92 deixada, sintaxe de junção externa completa e à direita. É a sequência de escape de junções externas  
  
 **{oj** _junção externa_**}**  
  
 em que *junção externa* é  
  
 *referência de tabela* {**esquerda &#124; direita &#124; completo} junção externa** {*referência de tabela* &#124; *junção externa*} **ON**  *critério de pesquisa*  
  
 *referência de tabela* Especifica um nome de tabela, e *critério de pesquisa* Especifica a condição de junção entre as *referências de tabela*.  
  
 Uma solicitação de junção externa deve aparecer após o **FROM** palavra-chave e antes do **onde** cláusula (se houver). Para obter informações de sintaxe completa, consulte [Outer Join sequência de Escape](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) no Apêndice c: Gramática SQL.  
  
 Por exemplo, as seguintes instruções SQL criam o mesmo conjunto de resultados que lista todos os clientes e mostra que tem pedidos abertos. A primeira instrução usa a sintaxe de sequência de escape. A segunda instrução usa a sintaxe de nativa para Oracle e não é interoperável.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Para determinar os tipos de junções externas que dão suporte a uma fonte de dados e o driver, um aplicativo chama **SQLGetInfo** com o SQL_OJ_CAPABILITIES flag. Os tipos de junções externas que podem ter suporte estão à esquerda, à direita, completo ou junções externas; aninhadas junções externas no qual os nomes de coluna na **ON** cláusula não tem a mesma ordem que os nomes de tabela respectivo na **OUTER JOIN** cláusula; junções internas em conjunto com junções externas; e junções externas usando qualquer operador de comparação ODBC. Se o tipo de informação SQL_OJ_CAPABILITIES retornar 0, não há suporte para nenhuma cláusula de junção externa.
