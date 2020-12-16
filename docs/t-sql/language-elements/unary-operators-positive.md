---
description: + (Adição unária) (Transact-SQL)
title: + (Adição unária) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- + (positive)
- +
- positive
dev_langs:
- TSQL
helpviewer_keywords:
- + (positive operator)
- positive operator (+)
- positive values [SQL Server]
ms.assetid: 0f31c5cc-3078-4f6a-9870-7eb1a98053fb
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ec7815d623208c5e2860fd233ba5a290e2e8762b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460899"
---
# <a name="unary-operators---positive"></a>Operadores unários – positivo
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

Retorna o valor de uma expressão numérica (um operador unário). Os operadores unários desempenham uma operação em apenas uma expressão de qualquer um dos tipos de dados da categoria de tipo de dados numéricos.   
  
|Operador|Significado|  
|--------------|-------------|  
|[+ (Positivo)](../../t-sql/language-elements/unary-operators-positive.md)|Valor numérico é positivo.|  
|[- (Negativo)](../../t-sql/language-elements/unary-operators-negative.md)|Valor numérico é negativo.|  
|[~ (Não de bit a bit)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|Retorna os complementos do número.|  
  
 Os operadores + (Positivo) e – (Negativo) podem ser usados em qualquer expressão de qualquer um dos tipos de dados da categoria de tipo de dados numérico. O operador ~ (NOT bit a bit) pode ser usado somente nas expressões de qualquer um dos tipos de dados da categoria de tipo de dados inteiros.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
+ numeric_expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *numeric_expression*  
 É qualquer [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida de um dos tipos de dados da categoria de tipo de dados numéricos, com exceção dos tipos de dados **datetime** e **smalldatetime**.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados de *numeric_expression*.  
  
## <a name="remarks"></a>Comentários  
 Embora uma adição unária possa aparecer antes de qualquer expressão numérica, nenhuma operação é executada no valor retornado da expressão. Especificamente, não retornará o valor positivo de uma expressão negativa. Para retornar o valor positivo de uma expressão negativa, use a função [ABS](../../t-sql/functions/abs-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-a-variable-to-a-positive-value"></a>a. Definindo uma variável como um valor positivo  
 O exemplo a seguir define uma variável como um valor positivo.  
  
```sql  
DECLARE @MyNumber DECIMAL(10,2);  
SET @MyNumber = +123.45;  
SELECT @MyNumber;  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
-----------   
123.45            
  
(1 row(s) affected)  
```  
  
### <a name="b-using-the-unary-plus-operator-with-a-negative-value"></a>B. Usando o operador de adição unária com um valor negativo  
 O exemplo a seguir mostra o uso da adição unária com uma expressão negativa e da função ABS() na mesma expressão negativa. A adição unária não afeta a expressão, mas a função ABS retorna o valor positivo da expressão.  
  
```sql  
USE tempdb;  
GO  
DECLARE @Num1 INT;  
SET @Num1 = -5;  
SELECT +@Num1, ABS(@Num1);  
GO  
```  
  
 Este é o conjunto de resultados:  
  
```  
----------- -----------  
-5          5  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [ABS &#40;Transact-SQL&#41;](../../t-sql/functions/abs-transact-sql.md)  
  
  
