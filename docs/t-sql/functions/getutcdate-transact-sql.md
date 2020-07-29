---
title: GETUTCDATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/02/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GETUTCDATE
- GETUTCDATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], UTC time
- dates [SQL Server], functions
- UTC time [SQL Server]
- date and time [SQL Server], GETUTCDATE
- Universal Time Coordinate [SQL Server]
- GETUTCDATE function [SQL Server]
- current date and time [SQL Server]
- time [SQL Server], current
- Greenwich Mean Time [SQL Server]
- functions [SQL Server], time
- system date and time [SQL Server]
- current UTC date and time [SQL Server]
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- dates [SQL Server], system date and time
- time [SQL Server], system
ms.assetid: 48a5b230-102e-4a89-bb2a-fcf0cac862bb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0979bf4241c24477274d7a220f7a4687339ab1e4
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112691"
---
# <a name="getutcdate-transact-sql"></a>GETUTCDATE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna o carimbo de data/hora atual do sistema de banco de dados como um valor **datetime**. O deslocamento de fuso horário do banco de dados não está incluído. Esse valor representa a hora UTC (Tempo Universal Coordenado) atual. Esse valor é derivado do sistema operacional do computador no qual a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada.  
  
> [!NOTE]  
>  SYSDATETIME e SYSUTCDATETIME têm mais precisão de segundos fracionários que GETDATE e GETUTCDATE. SYSDATETIMEOFFSET inclui o deslocamento de fuso horário do sistema. SYSDATETIME, SYSUTCDATETIME e SYSDATETIMEOFFSET podem ser atribuídos a uma variável de qualquer um dos tipos de data e hora.  
  
 Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
GETUTCDATE()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 **datetime**  
  
## <a name="remarks"></a>Comentários  
 Instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] podem se referir a GETUTCDATE sempre que puderem fazer referência a uma expressão **datatime**.  
  
 GETUTCDATE é uma função não determinística. Exibições e expressões que fazem referência a essa função em uma coluna não podem ser indexadas.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir usam as seis funções do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que retornam a data e a hora atuais para retornar a data, a hora ou ambas. Os valores são retornados em série; portanto, seus segundos fracionários podem ser diferentes.  
  
### <a name="a-getting-the-current-system-date-and-time"></a>a. Obtendo a data e a hora atuais do sistema  
  
```  
SELECT 'SYSDATETIME()      ', SYSDATETIME();  
SELECT 'SYSDATETIMEOFFSET()', SYSDATETIMEOFFSET();  
SELECT 'SYSUTCDATETIME()   ', SYSUTCDATETIME();  
SELECT 'CURRENT_TIMESTAMP  ', CURRENT_TIMESTAMP;  
SELECT 'GETDATE()          ', GETDATE();  
SELECT 'GETUTCDATE()       ', GETUTCDATE();  
/* Returned:  
SYSDATETIME()            2007-05-03 18:34:11.9351421  
SYSDATETIMEOFFSET()      2007-05-03 18:34:11.9351421 -07:00  
SYSUTCDATETIME()         2007-05-04 01:34:11.9351421  
CURRENT_TIMESTAMP        2007-05-03 18:34:11.933  
GETDATE()                2007-05-03 18:34:11.933  
GETUTCDATE()             2007-05-04 01:34:11.933  
*/  
```  
  
### <a name="b-getting-the-current-system-date"></a>B. Obtendo a data atual do sistema  
  
```  
SELECT 'SYSDATETIME()      ', CONVERT (date, SYSDATETIME());  
SELECT 'SYSDATETIMEOFFSET()', CONVERT (date, SYSDATETIMEOFFSET());  
SELECT 'SYSUTCDATETIME()   ', CONVERT (date, SYSUTCDATETIME());  
SELECT 'CURRENT_TIMESTAMP  ', CONVERT (date, CURRENT_TIMESTAMP);  
SELECT 'GETDATE()          ', CONVERT (date, GETDATE());  
SELECT 'GETUTCDATE()       ', CONVERT (date, GETUTCDATE());  
  
/* Returned:   
SYSDATETIME()            2007-05-03  
SYSDATETIMEOFFSET()      2007-05-03  
SYSUTCDATETIME()         2007-05-04  
CURRENT_TIMESTAMP        2007-05-03  
GETDATE()                2007-05-03  
GETUTCDATE()             2007-05-04  
*/  
```  
  
### <a name="c-getting-the-current-system-time"></a>C. Obtendo a hora atual do sistema  
  
```  
SELECT 'SYSDATETIME()      ', CONVERT (time, SYSDATETIME());  
SELECT 'SYSDATETIMEOFFSET()', CONVERT (time, SYSDATETIMEOFFSET());  
SELECT 'SYSUTCDATETIME()   ', CONVERT (time, SYSUTCDATETIME());  
SELECT 'CURRENT_TIMESTAMP  ', CONVERT (time, CURRENT_TIMESTAMP);  
SELECT 'GETDATE()          ', CONVERT (time, GETDATE());  
SELECT 'GETUTCDATE()       ', CONVERT (time, GETUTCDATE());  
/* Returned  
SYSDATETIME()            18:25:01.6958841  
SYSDATETIMEOFFSET()      18:25:01.6958841  
SYSUTCDATETIME()         01:25:01.6958841  
CURRENT_TIMESTAMP        18:25:01.6930000  
GETDATE()                18:25:01.6930000  
GETUTCDATE()             01:25:01.6930000  
*/  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


