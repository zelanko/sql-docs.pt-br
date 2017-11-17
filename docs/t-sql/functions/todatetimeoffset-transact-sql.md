---
title: TODATETIMEOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 6c0ff45ae5842950d9f15d7b131ad107fba351b5
ms.contentlocale: pt-br
ms.lasthandoff: 10/24/2017

---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um **datetimeoffset** valor que é convertido de um **datetime2** expressão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) que resolve para um [datetime2](../../t-sql/data-types/datetime2-transact-sql.md) valor.  
  
> [!NOTE]  
>  A expressão não pode ser do tipo **texto**, **ntext**, ou **imagem** porque esses tipos não podem ser convertidos implicitamente em **varchar** ou **nvarchar**.  
  
 *fuso_horário*  
 É uma expressão que representa o deslocamento de fuso horário em minutos (se for um inteiro), por exemplo -120, ou horas e minutos (se for uma cadeia de caracteres), por exemplo ‘+13.00’. O intervalo é de +14 a -14 (em horas). A expressão é interpretada em hora local para time_zone especificado.  
  
> [!NOTE]  
>  Se a expressão for uma cadeia de caracteres, deve estar no formato {+|-}TZH:THM.  
  
## <a name="return-type"></a>Tipo de retorno  
 **DateTimeOffset**. A precisão fracionária é igual a *datetime* argumento.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. Alterando o deslocamento de fuso horário da data e da hora atuais  
 O exemplo seguinte altera o deslocamento de fuso horário da data e da hora atuais para o fuso horário `-07:00`.  
  
```  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2007-08-30 15:51:34.7030000 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>B. Alterando o deslocamento de fuso horário em minutos  
 O exemplo seguinte altera o fuso horário atual para `-120` minutos.  
  
```  
DECLARE @todaysDate datetime2;  
SET @todaysDate = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDate, -120);  
-- RETURNS 2007-08-30 15:52:37.8770000 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. Adicionando um deslocamento de fuso horário de 13 horas  
 O exemplo seguinte adiciona um deslocamento de fuso horário de 13 horas a uma data e hora.  
  
```  
DECLARE @dateTime datetimeoffset(7)= '2007-08-28 18:00:30';  
SELECT TODATETIMEOFFSET (@dateTime, '+13:00');  
-- RETURNS 2007-08-28 18:00:30.0000000 +13:00  
```  
  
## <a name="see-also"></a>Consulte também  
 [CAST e CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Dados de data e hora tipos e funções &#40; Transact-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [FUSO horário &AMP;#40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


