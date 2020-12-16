---
description: '- (Negativo) (Transact-SQL)'
title: '- (Negative) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- negative
dev_langs:
- TSQL
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
- negative values
ms.assetid: d6c14d14-d379-403b-82db-c197ad58c896
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 77604125d1f69c09283148b59f2dfbdda7f62546
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462317"
---
# <a name="unary-operators---negative"></a>Operadores unários – Negative
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna o negativo do valor de uma expressão numérica (um operador unário). Os operadores unários desempenham uma operação em apenas uma expressão de qualquer um dos tipos de dados da categoria de tipo de dados numéricos.   
  
|Operador|Significado|  
|--------------|-------------|  
|[+ (Positivo)](../../t-sql/language-elements/unary-operators-positive.md)|Valor numérico é positivo.|  
|[- (Negativo)](../../t-sql/language-elements/unary-operators-negative.md)|Valor numérico é negativo.|  
|[~ (Não de bit a bit)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|Retorna os complementos do número.|  
  
 Os operadores + (Positivo) e – (Negativo) podem ser usados em qualquer expressão de qualquer um dos tipos de dados da categoria de tipo de dados numérico. O operador ~ (NOT bit a bit) pode ser usado somente nas expressões de qualquer um dos tipos de dados da categoria de tipo de dados inteiros. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
- numeric_expression  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *numeric_expression*  
 É qualquer [expressão](../../t-sql/language-elements/expressions-transact-sql.md) válida de qualquer tipo de dados da categoria de tipo de dados numéricos, exceto a categoria de data e hora.  
  
## <a name="result-types"></a>Tipos de resultado  
 Retorna o tipo de dados de *numeric_expression*, exceto que uma expressão **tinyint** sem sinal é promovida a um resultado **smallint** com sinal.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-a-variable-to-a-negative-value"></a>a. Definindo uma variável como um valor negativo  
 O exemplo a seguir define uma variável como um valor negativo.  
  
```sql 
USE tempdb;  
GO  
DECLARE @MyNumber DECIMAL(10,2);  
SET @MyNumber = -123.45;  
SELECT @MyNumber AS NegativeValue;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
NegativeValue  
---------------------------------------  
-123.45  
  
(1 row(s) affected)  
  
```  
  
### <a name="b-changing-a-variable-to-a-negative-value"></a>B. Alterando uma variável para um valor negativo  
 O exemplo a seguir altera uma variável para um valor negativo.  
  
```sql  
USE tempdb;  
GO  
DECLARE @Num1 INT;  
SET @Num1 = 5;  
SELECT @Num1 AS VariableValue, -@Num1 AS NegativeValue;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
VariableValue NegativeValue  
------------- -------------  
5             -5  
  
(1 row(s) affected)  
  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-the-negative-of-a-positive-constant"></a>C. Retornando o negativo de uma constante positiva  
 O exemplo a seguir retorna o negativo de uma constante positiva.  
  
```sql  
USE ssawPDW;  
  
SELECT TOP (1) - 17 FROM DimEmployee;  
```  
  
 Retornos  
  
```  
-17  
```  
  
### <a name="d-returning-the-positive-of-a-negative-constant"></a>D. Retornando o positivo de uma constante negativa  
 O exemplo a seguir retorna o positivo de uma constante negativa.  
  
```sql  
USE ssawPDW;  
  
SELECT TOP (1) - ( - 17) FROM DimEmployee;  
```  
  
 Retornos  
  
```  
17  
```  
  
### <a name="e-returning-the-negative-of-a-column"></a>E. Retornando o negativo de uma coluna  
 O exemplo a seguir retorna o negativo do valor de `BaseRate` para cada funcionário da tabela `dimEmployee`.  
  
```sql  
USE ssawPDW;  
  
SELECT - BaseRate FROM DimEmployee;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  

