---
title: DATETIMEOFFSETFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1c8a5f8bea3bf6ca97e0f7b4a35f8f78315716df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Retorna um valor de **datetimeoffset** para a data e hora especificadas e com deslocamentos e precisão especificados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
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
  
*minute*  
Expressão de inteiro que especifica minutos.
  
*segundos*  
Expressão de inteiro que especifica segundos.
  
*fractions*  
Expressão de inteiro que especifica frações.
  
*hour_offset*  
Expressão de inteiro que especifica a parte de hora do deslocamento de fuso horário.
  
*minute_offset*  
Expressão de inteiro que especifica a parte de minutos do deslocamento de fuso horário.
  
*precisão*  
Literal de inteiro que especifica a precisão do valor de **datetimeoffset** a ser retornado.
  
## <a name="return-types"></a>Tipos de retorno
**datetimeoffset(** *precision* **)**
  
## <a name="remarks"></a>Remarks  
**DATETIMEOFFSETFROMPARTS** retorna um tipo de dados **datetimeoffset** totalmente inicializado. Os argumentos de deslocamento são usados para representar o deslocamento de fuso horário. Se os argumentos de deslocamento forem omitidos, será assumido que o deslocamento de fuso horário é 00:00, ou seja, não há deslocamento de fuso horário. Se os argumentos de deslocamento forem especificados, ambos os argumentos devem estar presentes e ambos devem ser positivos ou negativos. Se *minute_offset* for especificado sem *hour_offset*, um erro será gerado. Se outros argumentos não forem válidos, um erro será lançado. Se os argumentos obrigatórios forem nulos, nulo será retornado. Porém, se o argumento *precision* for nulo, um erro será gerado.
  
O argumento *fractions* depende do argumento *precision*. Por exemplo, se *precision* for 7, cada fração representará 100 nanosegundos; se *precision* for 3, cada fração representará um milissegundo. Se o valor de *precision* for zero, o valor de *fractions* também deverá ser zero; caso contrário, um erro será gerado.
  
Essa função é capaz de ser remota para servidores do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e acima. Ela não será remota para servidores que têm uma versão anterior ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. Exemplo simples sem frações de um segundo  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2010, 12, 31, 14, 23, 23, 0, 12, 0, 7 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------------------------  
2010-12-07 00:00:00.0000000 +00:00  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. Exemplo simples com frações de um segundo  
O seguinte exemplo demonstra o uso dos parâmetros *fractions* e *precision*:
1.   Quando *fractions* tem um valor igual a 5 e *precision* tem um valor igual a 1, o valor de *fractions* representa 5/10 de um segundo.  
1.   Quando *fractions* tem um valor igual a 50 e *precision* tem um valor igual a 2, o valor de *fractions* representa 50/100 de um segundo.  
1.   Quando *fractions* tem um valor igual a 500 e *precision* tem um valor igual a 3, o valor de *fractions* representa 500/1.000 de um segundo.  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 5, 12, 30, 1 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 50, 12, 30, 2 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 500, 12, 30, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------------------  
2011-08-15 14:30:00.5 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.50 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.500 +12:30  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também
[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  


