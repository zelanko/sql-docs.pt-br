---
title: '@@DATEFIRST (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATE_FORMAT_TSQL
- DATE FORMAT
- '@@DATEFIRST_TSQL'
- '@@DATEFIRST'
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SET DATEFIRST
- first day of week [SQL Server]
- dates [SQL Server], first day of week
- day of week [SQL Server]
- SET DATEFIRST option [SQL Server]
- date and time [SQL Server], DATEFIRST
- DATEFIRST option [SQL Server]
- date and time [SQL Server], @@DATEFIRST
- weekdays [SQL Server]
- '@@DATEFIRST function [SQL Server]'
- functions [SQL Server], date and time
- options [SQL Server], date
ms.assetid: a178868e-49d5-4bd5-a5e2-1283409c8ce6
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 2dfe63f2d59cb3e3a1b563d524693af0d3dd1b51
ms.contentlocale: pt-br
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40datefirst-transact-sql"></a>& #x 40; & #x 40; DATEFIRST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna o valor atual, para uma sessão de [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [data e hora tipos de dados e funções &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```
@@DATEFIRST  
```  
  
## <a name="return-type"></a>Tipo de retorno  
**tinyint**
  
## <a name="remarks"></a>Comentários  
SET DATEFIRST especifica o primeiro dia da semana. O padrão do inglês dos EUA é 7, domingo.
  
A configuração desse idioma afeta a interpretação das cadeias de caracteres ao longo da conversão em valores de data para armazenamento no banco de dados, e a exibição dos valores de data armazenados no banco de dados. Essa configuração não afeta o formato de armazenamento de dados de data. No exemplo a seguir, o idioma é definido primeiramente como `Italian`. A instrução `SELECT @@DATEFIRST;` retorna `1`. O idioma é definido como `us_english`. A instrução `SELECT @@DATEFIRST;` retorna `7`.
  
```sql
SET LANGUAGE Italian;  
GO  
SELECT @@DATEFIRST;  
GO  
SET LANGUAGE us_english;  
GO  
SELECT @@DATEFIRST;  
```  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir define o primeiro dia da semana como `5` (sexta-feira) e assume o dia atual, `Today`, como sendo sábado. A instrução `SELECT` retorna o valor `DATEFIRST` e o número do dia atual da semana.
  
```sql
SET DATEFIRST 5;  
SELECT @@DATEFIRST AS 'First Day'  
    ,DATEPART(dw, SYSDATETIME()) AS 'Today';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
First Day         Today  
----------------  --------------  
5                 2  
```  
  
## <a name="example"></a>Exemplo
 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT @@DATEFIRST;  
```  
  
## <a name="see-also"></a>Consulte também
[Funções de configuração &#40; Transact-SQL &#41;](../../t-sql/functions/configuration-functions-transact-sql.md)
  
  


