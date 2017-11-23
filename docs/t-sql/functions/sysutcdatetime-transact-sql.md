---
title: SYSUTCDATETIME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/01/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYSUTCDATETIME
- SYSUTCDATETIME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- date and time [SQL Server], SYSUTCDATETIME
- SYSUTCDATETIME function [SQL Server]
- time [SQL Server], system
ms.assetid: f14fc2cd-9ea8-4daf-88f4-418cf523ab55
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7279e9d23cc57d433059b44e82b20eebd80e275b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysutcdatetime-transact-sql"></a>SYSUTCDATETIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um **datetime2** valor que contém a data e hora do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. A data e hora é retornada como hora UTC (Coordinated Universal Time). A especificação de precisão de segundo fracionária tem um intervalo de 1 a 7 dígitos. A precisão padrão é 7 dígitos.  
  
> [!NOTE]  
>  SYSDATETIME e SYSUTCDATE têm mais precisão de segundos fracionários que GETDATE e GETUTCDATE. SYSDATETIMEOFFSET inclui o deslocamento de fuso horário do sistema. SYSDATETIME, SYSUTCDATE e SYSDATETIMEOFFSET podem ser atribuídos a uma variável de qualquer um dos tipos de data e hora.  
  
 Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [funções de data e hora tipos de dados e](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SYSUTCDATETIME ( )  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 **datetime2**  
  
## <a name="remarks"></a>Comentários  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]instruções podem fazer referência a SYSUTCDATETIME em qualquer lugar, eles podem consultar um **datetime2** expressão.  
  
 SYSUTCDATETIME é uma função não determinística. Exibições e expressões que fazem referência a essa função em uma coluna não podem ser indexadas.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Obtém os valores de data e hora usando a API do Windows GetSystemTimeAsFileTime(). A precisão depende do hardware do computador e da versão do Windows no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada. A precisão desta API está fixada em 100 nanosegundos. A precisão pode ser determinada usando a API do Windows GetSystemTimeAdjustment().  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir usam as seis funções de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que retornam a data e a hora atuais para retornar a data, a hora ou ambas. Os valores são retornados em série; portanto, seus segundos fracionários podem ser diferentes.  
  
### <a name="a-showing-the-formats-that-are-returned-by-the-date-and-time-functions"></a>A. Mostrando os formatos que são retornados pelas funções de data e hora  
 O exemplo a seguir mostra os diferentes formatos que são retornados pelas funções de data e hora.  
  
```  
SELECT SYSDATETIME() AS SYSDATETIME  
    ,SYSDATETIMEOFFSET() AS SYSDATETIMEOFFSET  
    ,SYSUTCDATETIME() AS SYSUTCDATETIME  
    ,CURRENT_TIMESTAMP AS CURRENT_TIMESTAMP  
    ,GETDATE() AS GETDATE  
    ,GETUTCDATE() AS GETUTCDATE;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
SYSDATETIME()      2007-04-30 13:10:02.0474381
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047
GETDATE()          2007-04-30 13:10:02.047
GETUTCDATE()       2007-04-30 20:10:02.047
```  
  
### <a name="b-converting-date-and-time-to-date"></a>B. Convertendo data e hora em data  
 O exemplo a seguir mostra como converter valores de data e hora em `date`.  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
```  
  
### <a name="c-converting-date-and-time-values-to-time"></a>C. Convertendo valores de data e hora em hora  
 O exemplo a seguir mostra como converter valores de data e hora em `time`.  
  
 ```
DECLARE @DATETIME DATETIME = GetDate();
DECLARE @TIME TIME
SELECT @TIME = CONVERT(time, @DATETIME)
SELECT @TIME AS 'Time', @DATETIME AS 'Date Time'
```
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Time             Date Time  
13:49:33.6330000 2009-04-22 13:49:33.633
```  
  
## <a name="see-also"></a>Consulte também  
 [CAST e CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Dados de data e hora tipos e funções &#40; Transact-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [FUSO horário &AMP;#40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


