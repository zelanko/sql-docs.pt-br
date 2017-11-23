---
title: SET DATEFORMAT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEFORMAT
- SET DATEFORMAT
- SET_DATEFORMAT_TSQL
- DATEFORMAT_TSQL
dev_langs: TSQL
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
caps.latest.revision: "49"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3b1e233508eaedab627b57a3ce6938b90a9e196d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="set-dateformat-transact-sql"></a>SET DATEFORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Define a ordem das partes do mês, dia e ano para interpretar **data**, **smalldatetime**, **datetime**, **datetime2** e **datetimeoffset** cadeias de caracteres.  
  
 Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [data e hora tipos de dados e funções &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SET DATEFORMAT { format | @format_var }   
```  
  
## <a name="arguments"></a>Argumentos  
 *formato* | **@***format_var*  
 É a ordem das partes de data. Os parâmetros válidos são **MDA**, **DMA**, **ymd**, **ydm**, **myd**, e **dym**. Este argumento ou pode ser Unicode ou conjuntos de caracteres de dois bytes (DBCS) convertidos para Unicode. O padrão do Inglês dos EUA é **MDA**. Para o padrão DATEFORMAT de todas as linguagens de suporte, consulte [sp_helplanguage &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 DATEFORMAT **ydm** não há suporte para **data**, **datetime2** e **datetimeoffset** tipos de dados.  
  
 O efeito da configuração de DATEFORMAT na interpretação de cadeias de caracteres pode ser diferente para **datetime** e **smalldatetime** valores que **data**, **datetime2** e **datetimeoffset** valores, dependendo do formato de cadeia de caracteres. Esta configuração afeta a interpretação de cadeias de caracteres conforme elas são convertidas em valores de data para armazenamento no banco de dados. Ela não afeta a visualização de valores de tipo de dados de data que são armazenados no banco de dados ou o formato de armazenamento.  
  
 Alguns formatos de cadeias de caracteres são interpretados independentemente da configuração de DATEFORMAT, como ISO 8601, por exemplo.  
  
 A configuração de DATEFORMAT é definida no momento da execução e não no momento da análise.  
  
 SET DATEFORMAT anula a data implícita Formatar configuração [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

