---
title: DIA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DAY_TSQL
- DAY
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], DAY
- dates [SQL Server], functions
- DAY function [SQL Server]
- dates [SQL Server], days
- functions [SQL Server], date and time
- dateparts [SQL Server], day
ms.assetid: 2f4410ea-fd3e-4d69-ac4b-3b0091a084bc
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 9edfdc46ede4c090080c09253e2bb213a384816c
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna um inteiro que representa o dia (dia do mês) especificada *data*.
  
Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [data e hora tipos de dados e funções &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>Argumentos  
*date*  
É uma expressão que pode ser resolvida para um **tempo**, **data**, **smalldatetime**, **datetime**, **datetime2**, ou **datetimeoffset** valor. O *data* argumento pode ser uma expressão, a expressão de coluna, a variável definida pelo usuário ou a cadeia de caracteres literal.
  
## <a name="return-type"></a>Tipo de retorno  
**int**
  
## <a name="return-value"></a>Valor de retorno  
DAY retorna o mesmo valor como [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**dia**, *data*).
  
Se *data* contém apenas uma parte de hora, o valor de retorno é 1, o dia base.
  
## <a name="examples"></a>Exemplos  
A instrução a seguir retorna `30`. Este é o número do dia.
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
A instrução a seguir retorna `1900, 1, 1`. O argumento para *data* é o número `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como janeiro 1, 1900.
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  



