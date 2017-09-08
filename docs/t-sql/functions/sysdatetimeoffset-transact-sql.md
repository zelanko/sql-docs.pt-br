---
title: SYSDATETIMEOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYSDATETIMEOFFSET_TSQL
- SYSDATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], SYSDATETIMEOFFSET
- dates [SQL Server], functions
- current date and time [SQL Server]
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- SYSDATETIMEOFFSET function [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- dates [SQL Server], system date and time
- time zones [SQL Server]
- time [SQL Server], system
ms.assetid: 8423c753-cebe-4edd-871d-0138e092199f
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2497aa71cae4fa7cf5fecf6fe6bd1383d84680a1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="sysdatetimeoffset-transact-sql"></a>SYSDATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um **datetimeoffset(7)** valor que contém a data e hora do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. O deslocamento de fuso horário está incluído.  
  
 Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [data e hora tipos de dados e funções &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SYSDATETIMEOFFSET ( )  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 **DateTimeOffset(7)**  
  
## <a name="remarks"></a>Comentários  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]instruções podem se referir a SYSDATETIMEOFFSET em qualquer lugar, eles podem consultar um **datetimeoffset** expressão.  
  
 SYSDATETIMEOFFSET é uma função não determinística. Exibições e expressões que fazem referência a essa função em uma coluna não podem ser indexadas.  
  
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
  
 `SYSDATETIME()      2007-04-30 13:10:02.0474381`  
  
 `SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00`  
  
 `SYSUTCDATETIME()   2007-04-30 20:10:02.0474381`  
  
 `CURRENT_TIMESTAMP  2007-04-30 13:10:02.047`  
  
 `GETDATE()          2007-04-30 13:10:02.047`  
  
 `GETUTCDATE()       2007-04-30 20:10:02.047`  
  
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
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
### <a name="c-converting-date-and-time-to-times"></a>C. Convertendo valores de data e hora em horas  
 O exemplo a seguir mostra como converter valores de data e hora em `time`.  
  
```  
SELECT CONVERT (time, SYSDATETIME()) AS SYSDATETIME()  
    ,CONVERT (time, SYSDATETIMEOFFSET()) AS SYSDATETIMEOFFSET()  
    ,CONVERT (time, SYSUTCDATETIME()) AS SYSUTCDATETIME()  
    ,CONVERT (time, CURRENT_TIMESTAMP) AS CURRENT_TIMESTAMP  
    ,CONVERT (time, GETDATE()) AS GETDATE()  
    ,CONVERT (time, GETUTCDATE()) AS GETUTCDATE();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `SYSDATETIME()      13:18:45.3490361`  
  
 `SYSDATETIMEOFFSET()13:18:45.3490361`  
  
 `SYSUTCDATETIME()   20:18:45.3490361`  
  
 `CURRENT_TIMESTAMP  13:18:45.3470000`  
  
 `GETDATE()          13:18:45.3470000`  
  
 `GETUTCDATE()       20:18:45.3470000`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Os exemplos a seguir usam as seis funções de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que retornam a data e a hora atuais para retornar a data, a hora ou ambas. Os valores são retornados em série; portanto, seus segundos fracionários podem ser diferentes.  
  
### <a name="d-showing-the-formats-that-are-returned-by-the-date-and-time-functions"></a>D. Mostrando os formatos que são retornados pelas funções de data e hora  
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
  
 `SYSDATETIME()      2007-04-30 13:10:02.0474381`  
  
 `SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00`  
  
 `SYSUTCDATETIME()   2007-04-30 20:10:02.0474381`  
  
 `CURRENT_TIMESTAMP  2007-04-30 13:10:02.047`  
  
 `GETDATE()          2007-04-30 13:10:02.047`  
  
 `GETUTCDATE()       2007-04-30 20:10:02.047`  
  
### <a name="e-converting-date-and-time-to-date"></a>E. Convertendo data e hora em data  
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
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
### <a name="f-converting-date-and-time-to-times"></a>F. Convertendo valores de data e hora em horas  
 O exemplo a seguir mostra como converter valores de data e hora em `time`.  
  
```  
SELECT CONVERT (time, SYSDATETIME()) AS SYSDATETIME()  
    ,CONVERT (time, SYSDATETIMEOFFSET()) AS SYSDATETIMEOFFSET()  
    ,CONVERT (time, SYSUTCDATETIME()) AS SYSUTCDATETIME()  
    ,CONVERT (time, CURRENT_TIMESTAMP) AS CURRENT_TIMESTAMP  
    ,CONVERT (time, GETDATE()) AS GETDATE()  
    ,CONVERT (time, GETUTCDATE()) AS GETUTCDATE();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `SYSDATETIME()      13:18:45.3490361`  
  
 `SYSDATETIMEOFFSET()13:18:45.3490361`  
  
 `SYSUTCDATETIME()   20:18:45.3490361`  
  
 `CURRENT_TIMESTAMP  13:18:45.3470000`  
  
 `GETDATE()          13:18:45.3470000`  
  
 `GETUTCDATE()       20:18:45.3470000`  
  
## <a name="see-also"></a>Consulte também  
 [CAST e CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Dados de data e hora tipos e funções &#40; Transact-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  


