---
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26a8299165eea6a2a8f1b8d69f87dc92f9bf12b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65949071"
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um valor de **datetimeoffset** que é convertido de uma expressão **datetime2**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
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
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. Alterando o deslocamento de fuso horário da data e da hora atuais  
 O exemplo seguinte altera o deslocamento de fuso horário da data e da hora atuais para o fuso horário `-07:00`.  
  
```sql  
DECLARE @todaysDateTime datetime2;  
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
  
  

