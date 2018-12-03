---
title: SET DATEFORMAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEFORMAT
- SET DATEFORMAT
- SET_DATEFORMAT_TSQL
- DATEFORMAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], formats
- dates [SQL Server], ordering date parts
- SET DATEFORMAT option [SQL Server]
- DATEFORMAT option [SQL Server]
- date and time [SQL Server], SET DATEFORMAT
- options [SQL Server], date
- date and time [SQL Server], DATEFORMAT
- dateparts [SQL Server], dateformat
ms.assetid: da217878-7ec4-477e-aa13-604073c948f8
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6ce3a973f84664769ced971eedb28a1c13faeae8
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52519705"
---
# <a name="set-dateformat-transact-sql"></a>SET DATEFORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Define a ordem das partes do mês, dia e ano para interpretar cadeias de caracteres **date**, **smalldatetime**, **datetime**, **datetime2** e **datetimeoffset**.  
  
 Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SET DATEFORMAT { format | @format_var }   
```  
  
## <a name="arguments"></a>Argumentos  
 *format* | **@**_format_var_  
 É a ordem das partes de data. Os parâmetros válidos são **mdy**, **dmy**, **ymd**, **ydm**, **myd** e **dym**. Este argumento ou pode ser Unicode ou conjuntos de caracteres de dois bytes (DBCS) convertidos para Unicode. O padrão do O padrão em inglês é **mdy**. Para o DATEFORMAT padrão de todos os idiomas com suporte, consulte [sp_helplanguage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Não há suporte para DATEFORMAT **ydm** nos tipos de dados **date**, **datetime2** e **datetimeoffset**.  
  
 O efeito da configuração de DATEFORMAT na interpretação de cadeias de caracteres pode ser diferente para valores de **datetime** e **smalldatetime** comparado a valores **date**, **datetime2** e **datetimeoffset**, dependendo do formato da cadeia de caracteres. Esta configuração afeta a interpretação de cadeias de caracteres conforme elas são convertidas em valores de data para armazenamento no banco de dados. Ela não afeta a visualização de valores de tipo de dados de data que são armazenados no banco de dados ou o formato de armazenamento.  
  
 Alguns formatos de cadeias de caracteres são interpretados independentemente da configuração de DATEFORMAT, como ISO 8601, por exemplo.  
  
 A configuração de DATEFORMAT é definida no momento da execução e não no momento da análise.  
  
 SET DATEFORMAT substitui a configuração de formato de data implícita de [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O seguinte exemplo usa cadeias de datas diferentes como entradas em sessões com a mesma configuração `DATEFORMAT`.  
  
```  
-- Set date format to day/month/year.  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar datetime2 = '31/12/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: 2008-12-31 09:01:01.123  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar datetime2 = '12/31/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: Msg 241: Conversion failed when converting date and/or time -- from character string.  
  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

