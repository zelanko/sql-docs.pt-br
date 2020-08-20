---
description: NULL e UNKNOWN (Transact-SQL)
title: NULL e UNKNOWN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 9d491846-4730-4740-a680-77c69fae4a58
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb30710b35b1e82fafbc50dd7535b99be02ce5ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467552"
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
  
|Expressão 1|Expressão 2|Result|  
|---------------|---------------|------------|  
|TRUE|DESCONHECIDO|DESCONHECIDO|  
|DESCONHECIDO|DESCONHECIDO|DESCONHECIDO|  
|FALSE|DESCONHECIDO|FALSE|  
  
 A tabela a seguir mostra os resultados da aplicação de um operador OR para duas expressões boolianas, em que uma expressão retorna UNKNOWN.  
  
|Expressão 1|Expressão 2|Result|  
|---------------|---------------|------------|  
|TRUE|DESCONHECIDO|TRUE|  
|DESCONHECIDO|DESCONHECIDO|DESCONHECIDO|  
|FALSE|DESCONHECIDO|DESCONHECIDO|  
  
## <a name="see-also"></a>Consulte Também  
 [AND &#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [OR &#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  
