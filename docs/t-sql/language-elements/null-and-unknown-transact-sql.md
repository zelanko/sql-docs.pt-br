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
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bdac1899707b3caa4f4c515324511a47830f2722
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="null-and-unknown-transact-sql"></a>NULO e desconhecido (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL indica que o valor é desconhecido. Um valor nulo é diferente do valor um vazio ou zero. Dois valores nulos não são iguais. Comparações entre dois valores nulos, ou entre um valor nulo e qualquer outro valor, retornam unknown porque o valor de cada NULL é desconhecido.  
  
 Valores nulos geralmente indicam dados desconhecidos, não aplicável, ou a ser adicionado posteriormente. Por exemplo, é possível que a inicial do segundo nome de um cliente não seja conhecida no momento em que o cliente faz um pedido.  
  
 Observe o seguinte sobre valores nulos:  
  
-   Testar para obter valores null em uma consulta, use IS NULL ou IS NOT NULL na cláusula WHERE.  
  
-   Valores nulos podem ser inseridos em uma coluna declarando explicitamente NULL em uma instrução INSERT ou UPDATE ou omitindo uma coluna fora de uma instrução INSERT.  
  
-   Valores nulos não podem ser usados como as informações necessárias para distinguir uma linha em uma tabela de outra linha em uma tabela, como chaves primárias ou de informações usadas para distribuir as linhas, tais como chaves de distribuição.  
  
 Quando valores nulos estão presentes em dados, os operadores lógicos e de comparação podem potencialmente retornar um terceiro resultado UNKNOWN em vez de somente TRUE ou FALSE. Essa necessidade de lógica com valor três é uma fonte de muitos erros de aplicativo. Essas tabelas esboçam o efeito de introduzir comparações nulas.  
  
 A tabela a seguir mostra os resultados da aplicação de um operador AND a dois operandos boolianos onde um operando retorna NULL.  
  
|Operando 1|Operando 2|Resultado|  
|---------------|---------------|------------|  
|TRUE|NULL|FALSE|  
|NULL|NULL|FALSE|  
|FALSE|NULL|FALSE|  
  
 A tabela a seguir mostra os resultados da aplicação de um operador OR a dois operandos boolianos onde um operando retorna NULL.  
  
|Operando 1|Operando 2|Resultado|  
|---------------|---------------|------------|  
|TRUE|NULL|TRUE|  
|NULL|NULL|UNKNOWN|  
|FALSE|NULL|UNKNOWN|  
  
## <a name="see-also"></a>Consulte também  
 [E &#40; Transact-SQL &#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [OU &#40; Transact-SQL &#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [Não &#40; Transact-SQL &#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [É NULL &#40; Transact-SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  

