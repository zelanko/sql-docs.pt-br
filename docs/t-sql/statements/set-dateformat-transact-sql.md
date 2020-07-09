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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fbaa56a5e2c40523e925fa46a4e92e4fde283461
ms.sourcegitcommit: e6c260a139326f5a400a57ece812d39ef8b820bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86032504"
---
# <a name="set-dateformat-transact-sql"></a>SET DATEFORMAT (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Define a ordem das partes do mês, dia e ano para interpretar cadeias de caracteres de data. Essas cadeias de caracteres são do tipo **date**, **smalldatetime**, **datetime**, **datetime2** ou **datetimeoffset**.  
  
 Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
SET DATEFORMAT { format | @format_var }   
```  
  
## <a name="arguments"></a>Argumentos  
 *format* |  **@** _format_var_  
 É a ordem das partes de data. Os parâmetros válidos são **mdy**, **dmy**, **ymd**, **ydm**, **myd** e **dym**. Este argumento ou pode ser Unicode ou conjuntos de caracteres de dois bytes (DBCS) convertidos para Unicode. O padrão do inglês dos EUA O padrão em inglês é **mdy**. Para o DATEFORMAT padrão de todos os idiomas com suporte, consulte [sp_helplanguage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 O DATEFORMAT **ydm** não é compatível com os tipos de dados **date**, **datetime2** e **datetimeoffset**.  
  
 A configuração de DATEFORMAT pode interpretar cadeias de caracteres diferentes para tipos de dados de data, dependendo do formato da cadeia de caracteres desses dados. Por exemplo, interpretações de **datetime** e **smalldatetime** talvez não correspondam a **date**, **datetime2** ou **datetimeoffset**. DATEFORMAT afeta a interpretação de cadeias de caracteres conforme elas são convertidas em valores de data para o banco de dados. Ele não afeta a exibição de valores de tipo de dados de data, nem ao formato de armazenamento desses valores no banco de dados.  
  
 Alguns formatos de cadeia de caracteres são interpretados independentemente da configuração de DATEFORMAT, como ISO 8601, por exemplo.  
  
 A configuração de DATEFORMAT é definida no momento da execução e não no momento da análise.  
  
 SET DATEFORMAT substitui a configuração de formato de data implícita de [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O seguinte exemplo usa cadeias de datas diferentes como entradas em sessões com a mesma configuração `DATEFORMAT`.  
  
```sql
-- Set date format to day/month/year.  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar DATETIME2 = '31/12/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: 2008-12-31 09:01:01.123  
SET DATEFORMAT dmy;  
GO  
DECLARE @datevar DATETIME2 = '12/31/2008 09:01:01.1234567';  
SELECT @datevar;  
GO  
-- Result: Msg 241: Conversion failed when converting date and/or time -- from character string.  
  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  

