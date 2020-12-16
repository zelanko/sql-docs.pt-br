---
description: SWITCHOFFSET (Transact-SQL)
title: SWITCHOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/02/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dad555b6cd2e740d6d44f0dd4a3966f0e56e6b1b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461157"
---
# <a name="switchoffset-transact-sql"></a>SWITCHOFFSET (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna um valor **datetimeoffset** que é alterado do deslocamento de fuso horário armazenado para um novo deslocamento de fuso horário especificado.  
  
 Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
SWITCHOFFSET ( DATETIMEOFFSET, time_zone )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *DATETIMEOFFSET*  
 É uma expressão que pode ser resolvida em um valor **datetimeoffset(n)**.  
  
 *time_zone*  
 É uma cadeia de caracteres no formato [+|-]TZH:TZM ou um inteiro assinado (de minutos) que representa o deslocamento de fuso horário e que se pressupõe estar ajustado e reconhecer horário de verão.  
  
## <a name="return-type"></a>Tipo de retorno  
 **datetimeoffset** com a precisão fracionária do argumento *DATETIMEOFFSET*.  
  
## <a name="remarks"></a>Comentários  
 Use SWITCHOFFSET para selecionar um valor **datetimeoffset** em um deslocamento de fuso horário diferente do deslocamento de fuso horário originalmente armazenado. SWITCHOFFSET não atualiza o valor *time_zone* armazenado.  
  
 SWITCHOFFSET pode ser usado para atualizar uma coluna **datetimeoffset**.  
  
 Usar SWITCHOFFSET com a função GETDATE() pode fazer com que a consulta seja lenta. Isso ocorre porque o otimizador de consulta não pode obter estimativas de cardinalidade precisas para o valor de data e hora. Para resolver esse problema, use a dica de consulta OPTION (RECOMPILE) para forçar o otimizador de consulta a recompilar um plano de consulta na próxima vez que a mesma consulta for executada. O otimizador terá estimativas de cardinalidade exatas e gerará um plano de consulta mais eficiente. Para obter mais informações sobre a dica de consulta RECOMPILE, consulte [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
```sql
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
```  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `SWITCHOFFSET` para exibir um deslocamento de fuso horário diferente do valor armazenado no banco de dados.  
  
```sql  
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
  
## <a name="see-also"></a>Consulte Também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


