---
title: DATETIMEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATETIMEFROMPARTS_TSQL
- DATETIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEFROMPARTS function
ms.assetid: 6008148b-bf75-4c98-9392-68a89fa0711c
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 12c4107410cb0c482a24e40622d1858be9f7d1b2
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="datetimefromparts-transact-sql"></a>DATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Retorna um **datetime** valor para a data e hora especificadas.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATETIMEFROMPARTS ( year, month, day, hour, minute, seconds, milliseconds )  
```  
  
## <a name="arguments"></a>Argumentos  
*ano*  
Expressão de inteiro que especifica um ano.
  
*mês*  
Expressão de inteiro que especifica um mês.
  
*dia*  
Expressão de inteiro que especifica um dia.
  
*hora*  
Expressão de inteiro que especifica horas.
  
*minuto*  
Expressão de inteiro que especifica minutos.
  
*segundos*  
Expressão de inteiro que especifica segundos.
  
*milissegundos*  
Expressão de inteiro que especifica milissegundos.
  
## <a name="return-types"></a>Tipos de retorno
**datetime**
  
## <a name="remarks"></a>Comentários  
**DATETIMEFROMPARTS** retorna um completamente inicializado **datetime** valor. Se os argumentos não são válidos, um erro é gerado. Se os argumentos necessários forem nulos, null é retornado.
  
Essa função é capaz de ser remota para servidores do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e acima. Ela não será remota para servidores que têm uma versão anterior ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Exemplos  
  
```sql
SELECT DATETIMEFROMPARTS ( 2010, 12, 31, 23, 59, 59, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também
[Data e hora &#40; Transact-SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md)
  
  


