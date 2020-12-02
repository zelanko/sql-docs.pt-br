---
description: TODATETIMEOFFSET (Transact-SQL)
title: TODATETIMEOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TO_DATETIMEOFFSET_TSQL
- SWITCH_TZ_TSQL
- SWITCH_TZ
- TO_DATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], TODATETIMEOFFSET
- TODATETIMEOFFSET function
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: b5fafc08-efd4-4a3b-a0b3-068981a0a685
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 204cdfe73791ef1cf7e6d3b66ed20735b61e9b09
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91380447"
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna um valor de **datetimeoffset** que é convertido de uma expressão **datetime2**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *expressão*  
 É uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) resolvida em um valor [datetime2](../../t-sql/data-types/datetime2-transact-sql.md).  
  
> [!NOTE]  
>  A expressão não pode ser do tipo **text**, **ntext** ou **image** porque esses tipos não podem ser convertidos implicitamente em **varchar** ou **nvarchar**.  
  
 *time_zone*  
 É uma expressão que representa o deslocamento de fuso horário em minutos (se for um inteiro), por exemplo -120, ou horas e minutos (se for uma cadeia de caracteres), por exemplo '+13:00'. O intervalo é de +14 a -14 (em horas). A expressão é interpretada em hora local para time_zone especificado.  
  
> [!NOTE]  
>  Se a expressão for uma cadeia de caracteres, deve estar no formato {+|-}TZH:THM.  
  
## <a name="return-type"></a>Tipo de retorno  
 **datetimeoffset**. A precisão fracionária é igual à do argumento *datetime*.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>a. Alterando o deslocamento de fuso horário da data e da hora atuais  
 O exemplo seguinte altera o deslocamento de fuso horário da data e da hora atuais para o fuso horário `-07:00`.  
  
```sql  
DECLARE @todaysDateTime DATETIME2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2019-04-22 16:23:51.7666667 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>B. Alterando o deslocamento de fuso horário em minutos  
 O exemplo seguinte altera o fuso horário atual para `-120` minutos.  
  
```sql  
SELECT TODATETIMEOFFSET(SYSDATETIME(), -120)
-- RETURNS: 2019-04-22 11:39:21.6986813 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. Adicionando um deslocamento de fuso horário de 13 horas  
 O exemplo seguinte adiciona um deslocamento de fuso horário de 13 horas a uma data e hora.  
  
```sql  
SELECT TODATETIMEOFFSET(SYSDATETIME(), '+13:00')
-- RETURNS: 2019-04-22 11:39:29.0339301 +13:00
```  
  
## <a name="see-also"></a>Consulte Também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  

