---
description: DAY (Transact-SQL)
title: DAY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DAY_TSQL
- DAY
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], DAY
- dates [SQL Server], functions
- DAY function [SQL Server]
- dates [SQL Server], days
- functions [SQL Server], date and time
- dateparts [SQL Server], day
ms.assetid: 2f4410ea-fd3e-4d69-ac4b-3b0091a084bc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c785d96e43944e758627c948a5249971d05401be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88310802"
---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Esta função retorna um inteiro que representa o dia (dia do mês) da *date* especificada.
  
Consulte [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) para obter uma visão geral de todos os tipos de dados e funções de data e hora do [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DAY ( date )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*date*  
Uma expressão que é resolvida para um dos seguintes tipos de dados:

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

Para *date*, `DAY` aceitará uma variável de expressão de coluna, de expressão, de literal de cadeia de caracteres ou definida pelo usuário.
  
## <a name="return-type"></a>Tipo de retorno  
**int**
  
## <a name="return-value"></a>Valor retornado  
DAY retorna o mesmo valor que [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**day**, *date*).
  
Se *date* contiver apenas uma parte de hora, `DAY` retornará 1 – o dia base.
  
## <a name="examples"></a>Exemplos  
Esta instrução retorna `30` – o número do dia propriamente dito.
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
Esta instrução retorna `1900, 1, 1`. O argumento *date* tem um valor numérico de `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como janeiro 1, 1900.
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


