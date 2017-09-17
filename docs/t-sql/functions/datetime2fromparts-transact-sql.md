---
title: DATETIME2FROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c4ad800c684bcf69a52828969ca816a135901280
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Retorna um **datetime2** valor para a data e hora especificadas e com a precisão especificada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>Argumentos  
*ano*  
Expressão de inteiro que especifica um ano.
  
*mês*  
Expressão de inteiro que especifica um mês.
  
*dia*  
Expressão de inteiro que especifica um dia.
  
 *hora*  
Expressão de inteiro que especifica horas.
  
*minuto* expressão de inteiro que especifica minutos.
  
*segundos*  
Expressão de inteiro que especifica segundos.
  
*frações*  
Expressão de inteiro que especifica frações.
  
*precisão*  
Literal de inteiro que especifica a precisão do **datetime2** valor a ser retornado.
  
## <a name="return-types"></a>Tipos de retorno
**datetime2 (** *precisão* **)**
  
## <a name="remarks"></a>Comentários  
**DATETIME2FROMPARTS** retorna um completamente inicializado **datetime2** valor. Se os argumentos não são válidos, um erro será gerado. Se os argumentos necessários forem nulos, nulo será retornado. No entanto, se o *precisão* argumento for nulo, será gerado um erro.
  
O *frações* depende do argumento de *precisão* argumento. Por exemplo, se *precisão* for 7, cada fração representará 100 nanosegundos; se *precisão* é 3 e, em seguida, cada fração representará um milissegundo. Se o valor de *precisão* for zero, o valor de *frações* também deve ser zero; caso contrário, ocorrerá um erro.
  
Essa função é capaz de ser remota para servidores do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e acima. Ela não será remota para servidores que têm uma versão anterior ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. Exemplo simples sem frações de um segundo  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. Exemplo simples com frações de um segundo  
O exemplo a seguir demonstra o uso do *frações* e *precisão* parâmetros:
  
1.  Quando *frações* tem um valor de 5 e *precisão* tem um valor de 1, em seguida, o valor de *frações* representa 5 a 10 de segundo.  
  
2.  Quando *frações* tem um valor de 50 e *precisão* tem um valor de 2, em seguida, o valor de *frações* representa 50/100 de um segundo.  
  
3.  Quando *frações* tem um valor de 500 e *precisão* tem um valor de 3, em seguida, o valor de *frações* representará 500/1000 de um segundo.  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-example-without-fractions-of-a-second"></a>C. Exemplo simples sem frações de um segundo  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="d-example-with-fractions-of-a-second"></a>D. Exemplo simples com frações de um segundo  
O exemplo a seguir demonstra o uso do *frações* e *precisão* parâmetros:
1.  Quando *frações* tem um valor de 5 e *precisão* tem um valor de 1, em seguida, o valor de *frações* representa 5 a 10 de segundo.  
1.   Quando *frações* tem um valor de 50 e *precisão* tem um valor de 2, em seguida, o valor de *frações* representa 50/100 de um segundo.  
1.   Quando *frações* tem um valor de 500 e *precisão* tem um valor de 3, em seguida, o valor de *frações* representará 500/1000 de um segundo.  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também
[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)
  
  


