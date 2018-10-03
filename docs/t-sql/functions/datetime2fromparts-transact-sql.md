---
title: DATETIME2FROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d923e65f55edc56b2201d455567c924619dc0ad3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713534"
---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Essa função retorna um valor **datetime2** para os argumentos de data e hora especificados. O valor retornado tem uma precisão especificada pelo argumento precision.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>Argumentos  
*year*  
Uma expressão de inteiro que especifica um ano.
  
*month*  
Uma expressão de inteiro que especifica um mês.
  
*day*  
Uma expressão de inteiro que especifica um dia.
  
*hour*  
Uma expressão de inteiro que especifica as horas.
  
*minute*  
Uma expressão de inteiro que especifica os minutos.
  
*segundos*  
Uma expressão de inteiro que especifica os segundos.
  
*fractions*  
Uma expressão de inteiro que especifica um valor de segundos fracionário.
  
*precisão*  
Uma expressão de inteiro que especifica a precisão do valor **datetime2** que será retornado por `DATETIME2FROMPARTS`.
  
## <a name="return-types"></a>Tipos de retorno
**datetime2(** *precision* **)**
  
## <a name="remarks"></a>Remarks  
`DATETIME2FROMPARTS` retorna um valor **datetime2** completamente inicializado. `DATETIME2FROMPARTS` gerará um erro se pelo menos um argumento necessário tiver um valor inválido. `DATETIME2FROMPARTS` retornará nulo se pelo menos um argumento necessário tiver um valor nulo. No entanto, se o argumento *precision* tiver um valor nulo, `DATETIME2FROMPARTS` gerará um erro.

O argumento *fractions* depende do argumento *precision*. Por exemplo, para um valor de *precision* igual a 7, cada fração representará 100 nanossegundos; se *precision* for igual a 3, cada fração representará um milissegundo. Se o valor de *precision* for zero, o valor de *fractions* também deverá ser zero; caso contrário, `DATETIME2FROMPARTS` gerará um erro.
  
Essa função dá suporte à comunicação remota para servidores [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e acima. Ela não dará suporte a comunicação remota para servidores que têm uma versão anterior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-an-example-without-fractions-of-a-second"></a>A. Um exemplo sem frações de um segundo  
  
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
Este exemplo demonstra o uso dos parâmetros *fractions* e *precision*:
  
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
  
  

