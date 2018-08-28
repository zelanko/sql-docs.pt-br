---
title: DATETIMEOFFSETFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7dc04d4a8d1579f529cad6f8642d36610a856c41
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43078406"
---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Retorna um valor **datetimeoffset** para os argumentos de data e hora especificados. O valor retornado tem uma precisão especificada pelo argumento de precisão e um deslocamento conforme especificado pelos argumentos de deslocamento.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
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
  
*hour_offset*  
Uma expressão de inteiro que especifica a parte de hora da compensação de fuso horário.  
  
*minute_offset*  
Uma expressão de inteiro que especifica a parte de minuto da compensação de fuso horário.  
  
*precisão*  
Um valor literal de inteiro que especifica a precisão do valor **datetimeoffset** que `DATETIMEOFFSETFROMPARTS` retornará.  
  
## <a name="return-types"></a>Tipos de retorno
**datetimeoffset(** *precision* **)**  
  
## <a name="remarks"></a>Remarks  

`DATETIMEOFFSETFROMPARTS` retorna um tipo de dados **datetimeoffset** totalmente inicializado. Os argumentos de deslocamento representam o deslocamento de fuso horário. Para argumentos de deslocamento omitidos, `DATETIMEOFFSETFROMPARTS` presume um deslocamento de fuso horário de `00:00` – em outras palavras, nenhum deslocamento de fuso horário. Para argumentos de deslocamento especificados, `DATETIMEOFFSETFROMPARTS` espera valores para os argumentos e os dois valores devem ser positivos ou negativos. Se *minute_offset* tiver um valor e *hour_offset* não tiver um valor, `DATETIMEOFFSETFROMPARTS` gerará um erro. `DATETIMEOFFSETFROMPARTS` gerará um erro se outros argumentos tiverem valores inválidos. Se pelo menos um dos argumentos necessários tiver um valor `NULL`, `DATETIMEOFFSETFROMPARTS` retornará `NULL`. No entanto, se o argumento *precision* tiver um valor `NULL`, `DATETIMEOFFSETFROMPARTS` gerará um erro.  
  
O argumento *fractions* depende do argumento precision. Por exemplo, para um valor de 7, cada fração representará 100 nanossegundos; se precision for igual a 3, cada fração representará um milissegundo. Se o valor de precision for zero, o valor de fractions também deverá ser zero; caso contrário, `DATETIMEOFFSETFROMPARTS` gerará um erro.  
  
Essa função dá suporte à comunicação remota para servidores [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e acima. Ela não dará suporte a comunicação remota para servidores que têm uma versão anterior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-an-example-without-fractions-of-a-second"></a>A. Um exemplo sem frações de um segundo  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2010, 12, 31, 14, 23, 23, 0, 12, 0, 7 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------
2010-12-31 14:23:23.0000000 +12:00  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. Exemplo simples com frações de um segundo  

Este exemplo demonstra o uso dos parâmetros *fractions* e *precision*:  

1. Quando *fractions* tem um valor igual a 5 e *precision* tem um valor igual a 1, o valor de *fractions* representa 5/10 de um segundo.  

2. Quando *fractions* tem um valor igual a 50 e *precision* tem um valor igual a 2, o valor de *fractions* representa 50/100 de um segundo.  

3. Quando *fractions* tem um valor igual a 500 e *precision* tem um valor igual a 3, o valor de *fractions* representa 500/1.000 de um segundo.  
  
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
  
## <a name="see-also"></a>Confira também
[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  


