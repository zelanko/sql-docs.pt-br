---
description: '&#x40;&#x40;DATEFIRST (Transact-SQL)'
title: '@@DATEFIRST (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATE_FORMAT_TSQL
- DATE FORMAT
- '@@DATEFIRST_TSQL'
- '@@DATEFIRST'
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SET DATEFIRST
- first day of week [SQL Server]
- dates [SQL Server], first day of week
- day of week [SQL Server]
- SET DATEFIRST option [SQL Server]
- date and time [SQL Server], DATEFIRST
- DATEFIRST option [SQL Server]
- date and time [SQL Server], @@DATEFIRST
- weekdays [SQL Server]
- '@@DATEFIRST function [SQL Server]'
- functions [SQL Server], date and time
- options [SQL Server], date
ms.assetid: a178868e-49d5-4bd5-a5e2-1283409c8ce6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2f579cb44a2d938542b8e3a4d7fc177a495c85aa
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478697"
---
# <a name="x40x40datefirst-transact-sql"></a>&#x40;&#x40;DATEFIRST (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Essa função retorna o valor atual de [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md), para uma sessão específica.
  
Consulte [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) para obter uma visão geral de todos os tipos de dados e funções de data e hora do [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
@@DATEFIRST  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-type"></a>Tipo de retorno  
**tinyint**
  
## <a name="remarks"></a>Comentários  
SET DATEFIRST *n* Especifica o primeiro dia (DOMINGO, SEGUNDA-FEIRA, TERÇA-FEIRA, etc.) da semana. O valor de *n* varia de 1 a 7.

```sql
SET DATEFIRST 3;
GO  
SELECT @@DATEFIRST; -- 3 (Wednesday)
GO
```  

Para um ambiente em inglês (Estados Unidos), @@DATEFIRST assume o valor 7 (domingo) por padrão.
  
Essa configuração de idioma afeta a interpretação de cadeia de caracteres, já que o SQL Server converte essas cadeias de caracteres em valores de data para armazenamento de banco de dados. Essa configuração também afeta a exibição de valores de data armazenados no banco de dados. Essa configuração não impacta o formato de armazenamento de dados de data.

Este exemplo primeiro define o idioma para `Italian`. A instrução `SELECT @@DATEFIRST;` retorna `1`. A próxima instrução define o idioma para é então definido como `us_english`. A instrução final, `SELECT @@DATEFIRST;`, retorna `7`.
  
```sql
SET LANGUAGE Italian;  
GO  
SELECT @@DATEFIRST;  
GO  
SET LANGUAGE us_english;  
GO  
SELECT @@DATEFIRST;  
```  
  
## <a name="examples"></a>Exemplos  
Este exemplo define o primeiro dia da semana como `5` (sexta-feira) e assume o dia atual, `Today`, como sendo sábado. A instrução `SELECT` retorna o valor `DATEFIRST` e o número do dia atual da semana.
  
```sql
SET DATEFIRST 5;  
SELECT @@DATEFIRST AS 'First Day'  
    ,DATEPART(dw, SYSDATETIME()) AS 'Today';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
First Day         Today  
----------------  --------------  
5                 2  
```  
  
## <a name="example"></a>Exemplo
 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT @@DATEFIRST;  
```  
  
## <a name="see-also"></a>Confira também
[Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)
  
  

