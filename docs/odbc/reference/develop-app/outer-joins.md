---
title: Junções Externas | Microsoft Docs
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
ms.openlocfilehash: 81988d34dca38d5c041ff9f87e9674d7c97d76cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282437"
---
# <a name="outer-joins"></a>Junções externas
O ODBC suporta a sintaxe de adesão esquerda, direita e externa completa do SQL-92. A seqüência de fuga para as junções externas é  
  
 **{oj** _outer-join_**}**  
  
 onde *a adesão externa* é  
  
 *table-reference* {**LEFT &#124; RIGHT &#124; FULL} OUTER JOIN** {*table-reference* &#124; *outer-join*} **ON** _search-condition_  
  
 *a referência da tabela* especifica um nome da tabela e *a condição de pesquisa* especifica a condição de adesão entre as *referências de tabela*.  
  
 Uma solicitação de adesão externa deve aparecer após a palavra-chave **FROM** e antes da cláusula **WHERE** (se existir). Para obter informações completas sobre a sintaxe, consulte [Aseqüência de Escape de Junta externa](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) no apêndice C: Gramática SQL.  
  
 Por exemplo, as seguintes instruções SQL criam o mesmo conjunto de resultados que lista todos os clientes e mostra quais tem pedidos abertos. A primeira declaração usa a sintaxe de seqüência de fuga. A segunda declaração usa a sintaxe nativa para Oracle e não é interoperável.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Para determinar os tipos de adesão externa a uma fonte de dados e suporte ao driver, um aplicativo chama **sqlGetInfo** com a bandeira SQL_OJ_CAPABILITIES. Os tipos de adesões externas que podem ser suportadas são as junções externas esquerda, direita, completa ou aninhada; as junções externas nas quais os nomes das colunas na cláusula **ON** não têm a mesma ordem que seus respectivos nomes de tabela na cláusula **OUTER JOIN;** fusões internas em conjunto com as junções externas; e as junções externas usando qualquer operador de comparação ODBC. Se o SQL_OJ_CAPABILITIES tipo de informação retornar 0, nenhuma cláusula de adesão externa será suportada.
