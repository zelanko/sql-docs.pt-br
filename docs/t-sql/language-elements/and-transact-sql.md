---
description: AND (Transact-SQL)
title: AND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AND_TSQL
- AND
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], TRUE
- "TRUE"
- AND, about AND operators
- AND
- combining expressions
ms.assetid: b61d7f8d-5a51-49b7-91dd-f6190a5a0fb9
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c4d9a4169bac272cf57699a1436e36b53181e390
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124564"
---
# <a name="and-transact-sql"></a>AND (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Combina duas expressões boolianas e retorna **TRUE** quando ambas as expressões são **TRUE**. Quando mais de um operador lógico é usado em uma instrução, os operadores **AND** são avaliados primeiro. É possível alterar a ordem de avaliação usando parênteses.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
boolean_expression AND boolean_expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *boolean_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida que retorna um valor booliano: **TRUE**, **FALSE** ou **UNKNOWN**.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 Retorna TRUE quando as duas expressões são TRUE.  
  
## <a name="remarks"></a>Comentários  
 O gráfico a seguir mostra os resultados ao comparar valores TRUE e FALSE usando o operador AND.  
  
||TRUE|FALSE|DESCONHECIDO|  
|------|----------|-----------|-------------|  
|**TRUE**|TRUE|FALSE|DESCONHECIDO|  
|**FALSE**|FALSE|FALSE|FALSE|  
|**UNKNOWN**|DESCONHECIDO|FALSE|DESCONHECIDO|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-and-operator"></a>a. Usando o operador AND  
 O exemplo seguinte seleciona informações sobre funcionários que têm o título de `Marketing Assistant` e mais de `41` horas de férias disponíveis.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT  BusinessEntityID, LoginID, JobTitle, VacationHours   
FROM HumanResources.Employee  
WHERE JobTitle = 'Marketing Assistant'  
AND VacationHours > 41 ;  
```  
  
### <a name="b-using-the-and-operator-in-an-if-statement"></a>B. Usando o operador AND em uma instrução IF  
 Os exemplos seguintes mostram como usar AND em uma instrução IF. Na primeira instrução, `1 = 1` e `2 = 2` são verdadeiros; portanto, o resultado é true. No segundo exemplo, o argumento `2 = 17` é falso; portanto, o resultado é false.  
  
```sql  
IF 1 = 1 AND 2 = 2  
BEGIN  
   PRINT 'First Example is TRUE'  
END  
ELSE PRINT 'First Example is FALSE' ;  
GO  
  
IF 1 = 1 AND 2 = 17  
BEGIN  
   PRINT 'Second Example is TRUE'  
END  
ELSE PRINT 'Second Example is FALSE' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
