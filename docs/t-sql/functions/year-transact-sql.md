---
title: ANO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- YEAR
- YEAR_TSQL
dev_langs: TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server], years
- date and time [SQL Server], YEAR
- functions [SQL Server], date and time
- YEAR function [SQL Server]
- dateparts [SQL Server], year
ms.assetid: 74aa7ccc-8575-4018-80cf-14aeca379687
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 48dad4b2e38d9e178213aa8ad5ebb9e7608032a2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="year-transact-sql"></a>YEAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um inteiro que representa o ano da especificado *data*.  
  
 Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [data e hora tipos de dados e funções &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
YEAR ( date )  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 É uma expressão que pode ser resolvida para um **tempo**, **data**, **smalldatetime**, **datetime**, **datetime2**, ou **datetimeoffset** valor. O *data* argumento pode ser uma expressão, a expressão de coluna, a variável definida pelo usuário ou a cadeia de caracteres literal.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="return-value"></a>Valor de retorno  
 YEAR retorna o mesmo valor como [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**ano**, *data*).  
  
 Se *data* contém apenas uma parte de hora, o valor de retorno será 1900, o ano base.  
  
## <a name="examples"></a>Exemplos  
 A instrução a seguir retorna `2010`. Este é o número do ano.  
  
```  
SELECT YEAR('2010-04-30T01:01:01.1234567-07:00');  
```  
  
 A instrução a seguir retorna `1900, 1, 1`. O argumento para *data* é o número `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como janeiro 1, 1900.  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 A instrução a seguir retorna `1900, 1, 1`. O argumento para *data* é o número `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como janeiro 1, 1900.  
  
```  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>Consulte também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

