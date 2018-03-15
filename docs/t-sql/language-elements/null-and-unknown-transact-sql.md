---
title: NULL e UNKNOWN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 9d491846-4730-4740-a680-77c69fae4a58
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c26004fdfa5f2607235ffe7dddb7826a77f38b31
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="null-and-unknown-transact-sql"></a>NULL e UNKNOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL indica que o valor é desconhecido. Um valor nulo é diferente de um valor zero ou vazio. Dois valores nulos não são iguais. As comparações entre dois valores nulos ou entre um valor nulo e qualquer outro valor, retornam desconhecido porque o valor de cada NULL é desconhecido.  
  
 Os valores nulos geralmente indicam dados desconhecidos, não aplicáveis ou a serem adicionados posteriormente. Por exemplo, é possível que a inicial do segundo nome de um cliente não seja conhecida no momento em que o cliente faz um pedido.  
  
 Observe o seguinte sobre os valores nulos:  
  
-   Testar para obter valores null em uma consulta, use IS NULL ou IS NOT NULL na cláusula WHERE.  
  
-   Os valores nulos podem ser inseridos em uma coluna declarando explicitamente NULL em uma instrução INSERT ou UPDATE ou retirando uma coluna de uma instrução INSERT.  
  
-   Os valores nulos não podem ser usados como as informações necessárias para distinguir uma linha em uma tabela de outra linha em uma tabela, como chaves primárias, ou como as informações usadas para distribuir as linhas, como chaves de distribuição.  
  
 Quando valores nulos estão presentes em dados, os operadores lógicos e de comparação podem potencialmente retornar um terceiro resultado UNKNOWN em vez de somente TRUE ou FALSE. Essa necessidade de lógica com valor três é uma fonte de muitos erros de aplicativo. Os operadores lógicos em uma expressão booliana que incluírem UNKNOWNs retornarão UNKNOWN, a menos que o resultado do operador não dependa da expressão UNKNOWN. Estas tabelas fornecem exemplos desse comportamento.  
  
 A tabela a seguir mostra os resultados da aplicação de um operador AND para duas expressões boolianas, em que uma expressão retorna UNKNOWN.  
  
|Expressão 1|Expressão 2|Resultado|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|UNKNOWN|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|FALSE|  
  
 A tabela a seguir mostra os resultados da aplicação de um operador OR para duas expressões boolianas, em que uma expressão retorna UNKNOWN.  
  
|Expressão 1|Expressão 2|Resultado|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|TRUE|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|UNKNOWN|  
  
## <a name="see-also"></a>Consulte Também  
 [AND &#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [OR &#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  
