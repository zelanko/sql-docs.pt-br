---
title: NULO e desconhecido (Transact-SQL) | Microsoft Docs
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
# <a name="null-and-unknown-transact-sql"></a>NULO e desconhecido (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL indica que o valor é desconhecido. Um valor nulo é diferente do valor um vazio ou zero. Dois valores nulos não são iguais. Comparações entre dois valores nulos, ou entre um valor nulo e qualquer outro valor, retornam unknown porque o valor de cada NULL é desconhecido.  
  
 Valores nulos geralmente indicam dados desconhecidos, não aplicável, ou a ser adicionado posteriormente. Por exemplo, é possível que a inicial do segundo nome de um cliente não seja conhecida no momento em que o cliente faz um pedido.  
  
 Observe o seguinte sobre valores nulos:  
  
-   Testar para obter valores null em uma consulta, use IS NULL ou IS NOT NULL na cláusula WHERE.  
  
-   Valores nulos podem ser inseridos em uma coluna declarando explicitamente NULL em uma instrução INSERT ou UPDATE ou omitindo uma coluna fora de uma instrução INSERT.  
  
-   Valores nulos não podem ser usados como as informações necessárias para distinguir uma linha em uma tabela de outra linha em uma tabela, como chaves primárias ou de informações usadas para distribuir as linhas, tais como chaves de distribuição.  
  
 Quando valores nulos estão presentes em dados, os operadores lógicos e de comparação podem potencialmente retornar um terceiro resultado UNKNOWN em vez de somente TRUE ou FALSE. Essa necessidade de lógica com valor três é uma fonte de muitos erros de aplicativo. Operadores lógicos em uma expressão booleana que inclui desconhecidos retornará UNKNOWN, a menos que o resultado do operador não é dependente de expressão desconhecido. Essas tabelas fornecem exemplos desse comportamento.  
  
 A tabela a seguir mostra os resultados da aplicação de um operador AND para duas expressões booleanas onde uma expressão retorna UNKNOWN.  
  
|Expressão 1|Expressão 2|Resultado|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|UNKNOWN|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|FALSE|  
  
 A tabela a seguir mostra os resultados da aplicação de um operador OR para duas expressões booleanas onde uma expressão retorna UNKNOWN.  
  
|Expressão 1|Expressão 2|Resultado|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|TRUE|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|UNKNOWN|  
  
## <a name="see-also"></a>Consulte também  
 [AND &#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [OR &#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  
