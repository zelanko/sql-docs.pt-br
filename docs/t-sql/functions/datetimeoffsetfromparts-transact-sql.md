---
title: DATETIMEOFFSETFROMPARTS (Transact-SQL) | Microsoft Docs
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
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 665607c3b6ea9411d90137fba416d96d3d46a4c1
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Retorna um **datetimeoffset** valor para a data e hora especificadas e com os deslocamentos e precisão especificados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
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
  
*minuto*  
Expressão de inteiro que especifica minutos.
  
*segundos*  
Expressão de inteiro que especifica segundos.
  
*frações*  
Expressão de inteiro que especifica frações.
  
*hour_offset*  
Expressão de inteiro que especifica a parte de hora do deslocamento de fuso horário.
  
*minute_offset*  
Expressão de inteiro que especifica a parte de minutos do deslocamento de fuso horário.
  
*precisão*  
Literal de inteiro que especifica a precisão do **datetimeoffset** valor a ser retornado.
  
## <a name="return-types"></a>Tipos de retorno
**DateTimeOffset (** *precisão* **)**
  
## <a name="remarks"></a>Comentários  
**DATETIMEOFFSETFROMPARTS** retorna um completamente inicializado **datetimeoffset** tipo de dados. Os argumentos de deslocamento são usados para representar o deslocamento de fuso horário. Se os argumentos de deslocamento forem omitidos, será assumido que o deslocamento de fuso horário é 00:00, ou seja, não há deslocamento de fuso horário. Se os argumentos de deslocamento forem especificados, ambos os argumentos devem estar presentes e ambos devem ser positivos ou negativos. Se *minute_offset* for especificado sem *hour_offset*, um erro será gerado. Se outros argumentos não forem válidos, um erro será lançado. Se os argumentos necessários forem nulos, null é retornado. No entanto, se o *precisão* argumento for nulo, será gerado um erro.
  
O *frações* depende do argumento de *precisão* argumento. Por exemplo, se *precisão* for 7, cada fração representará 100 nanosegundos; se *precisão* é 3 e, em seguida, cada fração representará um milissegundo. Se o valor de *precisão* for zero, o valor de *frações* também deve ser zero; caso contrário, ocorrerá um erro.
  
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
O exemplo a seguir demonstra o uso do *frações* e *precisão* parâmetros:
1.   Quando *frações* tem um valor de 5 e *precisão* tem um valor de 1, em seguida, o valor de *frações* representa 5 a 10 de segundo.  
1.   Quando *frações* tem um valor de 50 e *precisão* tem um valor de 2, em seguida, o valor de *frações* representa 50/100 de um segundo.  
1.   Quando *frações* tem um valor de 500 e *precisão* tem um valor de 3, em seguida, o valor de *frações* representará 500/1000 de um segundo.  
  
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
[FUSO horário &AMP;#40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  



