---
title: ISDATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ISDATETIME
- ISDATE_TSQL
- ISDATE
- ISDATETIME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], ISDATE
- validate dates times [SQL Server]
- formats [SQL Server], time
- dates [SQL Server], validate
- verify dates times [SQL Server]
- functions [SQL Server], time
- formats [SQL Server], dates
- functions [SQL Server], date and time
- time [SQL Server], functions
- time [SQL Server], validate
- ISDATE function [SQL Server]
ms.assetid: 8e2c9ee7-388a-432f-b2c9-7b398f26bf85
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1385a80df97bc02af60cb5c151424dc79bd03913
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68109449"
---
# <a name="isdate-transact-sql"></a>ISDATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retornará 1 se a *expressão* for um valor **data**, **time** ou **datetime** válido; caso contrário, 0.  
  
 ISDATE retornará 0 se a *expressão* for um valor **datetime2**.  
  
 Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md). Observe que o intervalo de dados de data/hora será 1753-01-01 a 9999-12-31, quando o intervalo de dados de data for 0001-01-01 a 9999-12-31.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ISDATE ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É uma cadeia de caracteres ou [expressão](../../t-sql/language-elements/expressions-transact-sql.md) que pode ser convertida em cadeia de caracteres. A expressão deve ter menos de 4.000 caracteres. Os tipos de dados de data e hora, exceto datetime e smalldatetime, não são permitidos como o argumento para ISDATE.  
  
## <a name="return-type"></a>Tipo de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 ISDATE será determinista apenas se você usá-lo com a função [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md), se o parâmetro de estilo CONVERT for especificado e o estilo não for igual a 0, 100, 9 ou 109.  
  
 O valor retornado de ISDATE depende das configurações definidas por [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md), [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) e [Configurar idioma padrão da opção de configuração de servidor](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md).  
  
## <a name="isdate-expression-formats"></a>Formatos de expressão ISDATE  
 Para obter exemplos de formatos válidos para os quais ISDATE retornará 1, consulte a seção "Formatos de literal de cadeia de caracteres compatíveis com datetime" nos tópicos [datetime](../../t-sql/data-types/datetime-transact-sql.md) e [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md). Para obter outros exemplos, consulte também a coluna Entrada/Saída da seção "Argumentos" de [CAST e CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 A tabela a seguir resume os formatos de expressão de entrada que não são válidos e retornam 0 ou um erro.  
  
|Expressão ISDATE|Valor de retorno ISDATE|  
|-----------------------|-------------------------|  
|NULO|0|  
|Valores de tipos de dados listados em [Tipos de dados](../../t-sql/data-types/data-types-transact-sql.md) em qualquer categoria de tipo de dados que não cadeias de caracteres, cadeias de caracteres Unicode ou data e hora.|0|  
|Valores de tipos de dados **text**, **ntext** ou **image**.|0|  
|Qualquer valor que tenha uma escala de precisão de segundos maior que 3 (,0000 a ,0000000... n). ISDATE retornará 0 se a *expressão* for um valor **datetime2**, mas retornará 1 se a *expressão* for um valor **datetime** válido.|0|  
|Qualquer valor que combine uma data válida com um valor inválido, por exemplo 1995-10-1a.|0|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-isdate-to-test-for-a-valid-datetime-expression"></a>a. Usando ISDATE para testar uma expressão datetime válida  
 O exemplo a seguir mostra como usar `ISDATE` para testar se uma cadeia de caracteres é uma **datatime** válida.  
  
```  
IF ISDATE('2009-05-12 10:19:41.177') = 1  
    PRINT 'VALID'  
ELSE  
    PRINT 'INVALID';  
```  
  
### <a name="b-showing-the-effects-of-the-set-dateformat-and-set-language-settings-on-return-values"></a>B. Mostrando os efeitos das configurações SET DATEFORMAT e SET LANGUAGE em valores de retorno  
 As instruções a seguir mostram os valores retornados como resultado das configurações de `SET DATEFORMAT` e `SET LANGUAGE`.  
  
```  
/* Use these sessions settings. */  
SET LANGUAGE us_english;  
SET DATEFORMAT mdy;  
/* Expression in mdy dateformat */  
SELECT ISDATE('04/15/2008'); --Returns 1.  
/* Expression in mdy dateformat */  
SELECT ISDATE('04-15-2008'); --Returns 1.   
/* Expression in mdy dateformat */  
SELECT ISDATE('04.15.2008'); --Returns 1.   
/* Expression in myd  dateformat */  
SELECT ISDATE('04/2008/15'); --Returns 1.  
  
SET DATEFORMAT mdy;  
SELECT ISDATE('15/04/2008'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('15/2008/04'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('2008/15/04'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('2008/04/15'); --Returns 1.  
  
SET DATEFORMAT dmy;  
SELECT ISDATE('15/04/2008'); --Returns 1.  
SET DATEFORMAT dym;  
SELECT ISDATE('15/2008/04'); --Returns 1.  
SET DATEFORMAT ydm;  
SELECT ISDATE('2008/15/04'); --Returns 1.  
SET DATEFORMAT ymd;  
SELECT ISDATE('2008/04/15'); --Returns 1.  
  
SET LANGUAGE English;  
SELECT ISDATE('15/04/2008'); --Returns 0.  
SET LANGUAGE Hungarian;  
SELECT ISDATE('15/2008/04'); --Returns 0.  
SET LANGUAGE Swedish;  
SELECT ISDATE('2008/15/04'); --Returns 0.  
SET LANGUAGE Italian;  
SELECT ISDATE('2008/04/15'); --Returns 1.  
  
/* Return to these sessions settings. */  
SET LANGUAGE us_english;  
SET DATEFORMAT mdy;  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-isdate-to-test-for-a-valid-datetime-expression"></a>C. Usando ISDATE para testar uma expressão datetime válida  
 O exemplo a seguir mostra como usar `ISDATE` para testar se uma cadeia de caracteres é uma **datatime** válida.  
  
```  
IF ISDATE('2009-05-12 10:19:41.177') = 1  
    SELECT 'VALID';  
ELSE  
    SELECT 'INVALID';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

