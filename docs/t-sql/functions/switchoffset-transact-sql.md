---
title: SWITCHOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/02/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SWITCHTZ
- SWITCHTZ_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- functions [SQL Server], time
- functions [SQL Server], date and time
- SWITCHOFFSET function [SQL Server]
- time [SQL Server], functions
- date and time [SQL Server], SWITCHOFFSET
- time zones [SQL Server]
ms.assetid: 32a48e36-0aa4-4260-9fe9-cae9197d16c5
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 3c81153c233e68d12347dc47ae9c232f4a5ee030
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="switchoffset-transact-sql"></a>SWITCHOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um **datetimeoffset** valor é alterado do deslocamento de fuso horário armazenado para um novo deslocamento de fuso horário especificado.  
  
 Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [data e hora tipos de dados e funções &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SWITCHOFFSET ( DATETIMEOFFSET, time_zone )   
```  
  
## <a name="arguments"></a>Argumentos  
 *DATETIMEOFFSET*  
 É uma expressão que pode ser resolvida para um **DateTimeOffset (n)** valor.  
  
 *fuso_horário*  
 É uma cadeia de caracteres no formato [+|-]TZH:TZM ou um inteiro assinado (de minutos) que representa o deslocamento de fuso horário e que se pressupõe estar ajustado e reconhecer horário de verão.  
  
## <a name="return-type"></a>Tipo de retorno  
 **DateTimeOffset** com a precisão fracionária de *DATETIMEOFFSET* argumento.  
  
## <a name="remarks"></a>Comentários  
 Use SWITCHOFFSET para selecionar um **datetimeoffset** valor em um deslocamento de fuso horário diferente do deslocamento de fuso horário que foi originalmente armazenado. SWITCHOFFSET não atualiza o armazenado *fuso_horário* valor.  
  
 SWITCHOFFSET pode ser usado para atualizar um **datetimeoffset** coluna.  
  
 Usar SWITCHOFFSET com a função GETDATE() pode fazer com que a consulta seja lenta. Isso ocorre porque o otimizador de consulta não pode obter estimativas de cardinalidade precisas para o valor de data e hora. Para resolver esse problema, use a dica de consulta OPTION (RECOMPILE) para forçar o otimizador de consulta a recompilar um plano de consulta na próxima vez que a mesma consulta for executada. O otimizador terá estimativas de cardinalidade exatas e gerará um plano de consulta mais eficiente. Para obter mais informações sobre a dica de consulta RECOMPILE, consulte [dicas de consulta &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-query.md).  
  
```  
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
  
```  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `SWITCHOFFSET` para exibir um deslocamento de fuso horário diferente do valor armazenado no banco de dados.  
  
```  
CREATE TABLE dbo.test   
    (  
    ColDatetimeoffset datetimeoffset  
    );  
GO  
INSERT INTO dbo.test   
VALUES ('1998-09-20 7:45:50.71345 -5:00');  
GO  
SELECT SWITCHOFFSET (ColDatetimeoffset, '-08:00')   
FROM dbo.test;  
GO  
--Returns: 1998-09-20 04:45:50.7134500 -08:00  
SELECT ColDatetimeoffset  
FROM dbo.test;  
--Returns: 1998-09-20 07:45:50.7134500 -05:00  
```  
  
## <a name="see-also"></a>Consulte também  
 [CAST e CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [FUSO horário &AMP;#40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  



