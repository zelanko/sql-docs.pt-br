---
title: int, bigint, smallint e tinyint (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bigint_TSQL
- smallint
- bigint
- smallint_TSQL
- tinyint_TSQL
- int_TSQL
- int
- tinyint
dev_langs:
- TSQL
helpviewer_keywords:
- exact numeric data [SQL Server]
- numeric data
- tinyint data type
- int data type
- smallint data type
ms.assetid: 9bda5b0b-2380-4931-a1c8-f362fdefa99b
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46ac51971b07b38b73ef18d8a953674fc77b4b17
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="int-bigint-smallint-and-tinyint-transact-sql"></a>int, bigint, smallint e tinyint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de dados numéricos exatos que usam dados inteiros. Para economizar espaço no banco de dados, use o menor tipo de dados que confiável pode conter todos os valores possíveis. Por exemplo, tinyint seria suficiente para uma duração de pessoas, porque não existe para ter mais de 255 anos. Mas tinyint não seria suficiente para uma duração de construções, como uma construção pode ser mais de 255 anos de idade.
  
|Tipo de dados|Intervalo|Armazenamento|  
|---|---|---|
|**bigint**|-2^63 (-9.223.372.036.854.775.808) a 2^63-1 (9.223.372.036.854.775.807)|8 bytes|  
|**int**|-2^31 (-2.147.483.648) a 2^31-1 (2.147.483.647)|4 bytes|  
|**smallint**|-2^15 (-32.768) a 2^15-1 (32.767)|2 bytes|  
|**tinyint**|0 a 255|1 byte|  
  
## <a name="remarks"></a>Comentários  
O **int** tipo de dados é o tipo de dados de inteiro primário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O **bigint** tipo de dados é destinado ao uso quando valores inteiros possam exceder o intervalo que é compatível com o **int** tipo de dados.
  
**bigint** se encaixa entre **smallmoney** e **int** no gráfico de precedência de tipo de dados.
  
As funções retornam **bigint** somente se a expressão de parâmetro é um **bigint** tipo de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]não promove automaticamente outros tipos de dados inteiro (**tinyint**, **smallint**, e **int**) para **bigint**.
  
> [!CAUTION]  
>  Quando você usa o +, -, \*, /, ou os operadores aritméticos para executar a conversão implícita ou explícita de % **int**, **smallint**, **tinyint**, ou ** bigint** valores constantes para o **float**, **real**, **decimal** ou **numérico** tipos de dados, as regras que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplica ao calcular o tipo de dados e a precisão dos resultados da expressão diferem dependendo se a consulta for automaticamente parametrizada ou não.  
>   
>  Portanto, as expressões semelhantes em consultas podem, às vezes, produzir resultados diferentes. Quando uma consulta não for automaticamente parametrizada, o valor da constante é primeiro convertido em **numérico**, cuja precisão é grande o suficiente para conter o valor da constante, antes de converter o tipo de dados especificado. Por exemplo, o valor da constante 1 é convertido em **numérico (1, 0)**, e o valor constante 250 é convertido em **numérico (3, 0)**.  
>   
>  Quando uma consulta for automaticamente parametrizada, o valor da constante sempre é convertido em **numérico (10, 0)** antes de converter o tipo de dados final. Quando o operador / estiver envolvido, não apenas a precisão do tipo do resultado pode diferir entre consultas semelhantes, mas também o valor do resultado. Por exemplo, o valor do resultado de uma consulta automaticamente parametrizada que inclua a expressão `SELECT CAST (1.0 / 7 AS float)`, difere do valor do resultado da consulta mesmo que não é automaticamente parametrizada, porque os resultados da consulta automaticamente parametrizada, são truncados para se ajustar à o **numérico (10, 0)** tipo de dados.  
  
## <a name="converting-integer-data"></a>Convertendo dados inteiros
Quando integers são convertidos implicitamente em um tipo de dados character, se o integer for muito grande para ser ajustado no campo de caractere, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] digitará o caractere ASCII 42, o asterisco (*).
  
Constantes de inteiro maiores que 2.147.483.647 são convertidos para o **decimal** tipo de dados, não o **bigint** tipo de dados. O exemplo a seguir mostra que, quando o valor de limite for excedido, altera o tipo de dados do resultado de uma **int** para um **decimal**.
  
```sql
SELECT 2147483647 / 2 AS Result1, 2147483649 / 2 AS Result2 ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result1      Result2  
1073741823   1073741824.500000  
```  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir cria uma tabela usando o **bigint**, **int**, **smallint**, e **tinyint** tipos de dados. Os valores são inseridos em cada coluna e retornados na instrução SELECT.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyBigIntColumn bigint  
,MyIntColumn  int
,MySmallIntColumn smallint
,MyTinyIntColumn tinyint
);  
  
GO  
  
INSERT INTO dbo.MyTable VALUES (9223372036854775807, 2147483647,32767,255);  
 GO  
SELECT MyBigIntColumn, MyIntColumn, MySmallIntColumn, MyTinyIntColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyBigIntColumn       MyIntColumn MySmallIntColumn MyTinyIntColumn  
-------------------- ----------- ---------------- ---------------  
9223372036854775807  2147483647  32767            255  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

