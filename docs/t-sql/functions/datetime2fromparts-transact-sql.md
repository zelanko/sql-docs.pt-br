---
title: DATETIME2FROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e2b55cdb54537bafd171c1fd2d340ea679b2bcd2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Retorna um valor de **datetime2** para a data e hora especificadas e com a precisão especificada.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>Argumentos  
*year*  
Expressão de inteiro que especifica um ano.
  
*month*  
Expressão de inteiro que especifica um mês.
  
*day*  
Expressão de inteiro que especifica um dia.
  
 *hour*  
Expressão de inteiro que especifica horas.
  
Expressão de inteiro de *minute* que especifica minutos.
  
*segundos*  
Expressão de inteiro que especifica segundos.
  
*fractions*  
Expressão de inteiro que especifica frações.
  
*precisão*  
Literal de inteiro que especifica a precisão do valor de **datetime2** a ser retornado.
  
## <a name="return-types"></a>Tipos de retorno
**datetime2(** *precision* **)**
  
## <a name="remarks"></a>Remarks  
**DATETIME2FROMPARTS** retorna um valor de **datetime2** totalmente inicializado. Se os argumentos não forem válidos, um erro será gerado. Se os argumentos necessários forem nulos, nulo será retornado. Porém, se o argumento *precision* for nulo, um erro será gerado.
  
O argumento *fractions* depende do argumento *precision*. Por exemplo, se *precision* for 7, cada fração representará 100 nanosegundos; se *precision* for 3, cada fração representará um milissegundo. Se o valor de *precision* for zero, o valor de *fractions* também deverá ser zero; caso contrário, um erro será gerado.
  
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
O seguinte exemplo demonstra o uso dos parâmetros *fractions* e *precision*:
  
1.  Quando *fractions* tem um valor igual a 5 e *precision* tem um valor igual a 1, o valor de *fractions* representa 5/10 de um segundo.  
  
2.  Quando *fractions* tem um valor igual a 50 e *precision* tem um valor igual a 2, o valor de *fractions* representa 50/100 de um segundo.  
  
3.  Quando *fractions* tem um valor igual a 500 e *precision* tem um valor igual a 3, o valor de *fractions* representa 500/1.000 de um segundo.  
  
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
  
## <a name="see-also"></a>Confira também
[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)
  
  

