---
description: Junções externas
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9be14c2b7c0dd6cdebc458fd22dc090862eb9dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429118"
---
# <a name="outer-joins"></a>Junções externas
O ODBC dá suporte à sintaxe de junção externa do SQL-92 esquerda, direita e completa. A sequência de escape para junções externas é  
  
 **{OJ** _externa-junção_**}**  
  
 onde *a junção externa* é  
  
 *tabela-referência* {**esquerda &#124; direita &#124; Full} junção externa** {*tabela-referência* &#124; *externa-junção*} **na** _condição de pesquisa_  
  
 *tabela-referência* especifica um nome de tabela e a *condição de pesquisa* especifica a condição de junção entre as referências de *tabela*.  
  
 Uma solicitação de junção externa deve aparecer após a palavra-chave **from** e antes da cláusula **Where** (se houver). Para obter informações de sintaxe completas, consulte [sequência de escape de junção externa](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) no Apêndice C: gramática SQL.  
  
 Por exemplo, as instruções SQL a seguir criam o mesmo conjunto de resultados que lista todos os clientes e mostra o que tem pedidos abertos. A primeira instrução usa a sintaxe de sequência de escape. A segunda instrução usa a sintaxe nativa para Oracle e não é interoperável.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Para determinar os tipos de junções externas às quais uma fonte de dados e o driver dão suporte, um aplicativo chama **SQLGetInfo** com o sinalizador SQL_OJ_CAPABILITIES. Os tipos de junções externas que podem ter suporte são as junções esquerda, direita, completa ou externa aninhada; junções externas nas quais os nomes de coluna na cláusula **on** não têm a mesma ordem que seus respectivos nomes de tabela na cláusula de **junção externa** ; junções internas em conjunto com junções externas; e junções externas usando qualquer operador ODBC Comparison. Se o tipo de informação SQL_OJ_CAPABILITIES retorna 0, não há suporte para nenhuma cláusula de junção externa.
