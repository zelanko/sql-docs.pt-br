---
title: DATEFROMPARTS (Transact-SQL) | Microsoft Docs
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
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: a94584788187162e4cd7d433d71653a04c5103e2
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="datefromparts-transact-sql"></a>DATEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Retorna um **data** valor para o ano especificado, mês e dia.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATEFROMPARTS ( year, month, day )  
```  
  
## <a name="arguments"></a>Argumentos  
*ano*  
Expressão de inteiro que especifica um ano.
  
*mês*  
Expressão de inteiro que especifica um mês, de 1 a 12.
  
*dia*  
Expressão de inteiro que especifica um dia.
  
## <a name="return-types"></a>Tipos de retorno
**date**
  
## <a name="remarks"></a>Comentários  
**DATEFROMPARTS** retorna um **data** valor com a parte de data definida como o ano especificado, o mês e o dia e a parte de hora definida como o padrão. Se os argumentos não são válidos, um erro é gerado. Se os argumentos necessários forem nulos, nulo será retornado.
  
Essa função é capaz de ser remota para servidores do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e acima. Ela não será remota para servidores de versão anterior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir demonstra o **DATEFROMPARTS** função.
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também
[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)
  
  


