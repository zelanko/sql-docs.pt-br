---
title: int, bigint, smallint, and tinyint (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c61ca9f853f851bb531abdbcba66773f9e9d9e1e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077906"
---
# <a name="int-bigint-smallint-and-tinyint-transact-sql"></a>int, bigint, smallint e tinyint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de dados numéricos exatos que usam dados inteiros. Para economizar espaço no banco de dados, use o menor tipo de dados que pode conter todos os valores possíveis de maneira confiável. Por exemplo, tinyint é suficiente para a idade de uma pessoa porque não existe ninguém que viva por mais de 255 anos. Mas tinyint não é suficiente para a idade de um edifício, porque um edifício pode ter mais de 255 anos.
  
|Tipo de dados|Intervalo|Armazenamento|  
|---|---|---|
|**bigint**|-2^63 (-9.223.372.036.854.775.808) a 2^63-1 (9.223.372.036.854.775.807)|8 bytes|  
|**int**|-2^31 (-2.147.483.648) a 2^31-1 (2.147.483.647)|4 bytes|  
|**smallint**|-2^15 (-32.768) a 2^15-1 (32.767)|2 bytes|  
|**tinyint**|0 a 255|1 byte|  
  
## <a name="remarks"></a>Remarks  
O tipo de dados **int** é o tipo de dados inteiros primário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O tipo de dados **bigint** deve ser usado quando valores inteiros podem exceder o intervalo ao qual tipo de dados **int** dá suporte.
  
**bigint** se ajusta entre **smallmoney** e **int** no gráfico de precedência de tipo de dados.
  
As funções retornam **bigint** somente se a expressão de parâmetro é um tipo de dados **bigint**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não promove automaticamente outros tipos de dados inteiros (**tinyint**, **smallint** e **int**) para **bigint**.
  
> [!CAUTION]  
>  Ao usar os operadores aritméticos +, -, \*, / ou % para executar a conversão implícita ou explícita de valores constantes **int**, **smallint**, **tinyint** ou **bigint** nos tipos de dados **float**, **real**, **decimal** ou **numeric**, as regras que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica ao calcular o tipo de dados e a precisão dos resultados da expressão diferem, dependendo do fato de a consulta ser ou não automaticamente parametrizada.  
>   
>  Portanto, as expressões semelhantes em consultas podem, às vezes, produzir resultados diferentes. Quando uma consulta não é automaticamente parametrizada, o valor de constante é primeiramente convertido em **numeric**, cuja precisão é apenas grande o suficiente para conter o valor da constante, antes de fazer a conversão no tipo de dados especificado. Por exemplo, o valor de constante 1 é convertido em **numeric (1, 0)** e o valor de constante 250 é convertido em **numeric (3, 0)** .  
>   
>  Quando uma consulta é automaticamente parametrizada, o valor de constante sempre é convertido em **numeric (10, 0)** antes da conversão no tipo de dados final. Quando o operador / estiver envolvido, não apenas a precisão do tipo do resultado pode diferir entre consultas semelhantes, mas também o valor do resultado. Por exemplo, o valor do resultado de uma consulta automaticamente parametrizada que inclui a expressão `SELECT CAST (1.0 / 7 AS float)` diferirá do valor do resultado da mesma consulta que não é automaticamente parametrizada, porque os resultados da primeira serão truncados para se ajustarem ao tipo de dados **numeric (10, 0)** .  
  
## <a name="converting-integer-data"></a>Convertendo dados inteiros
Quando integers são convertidos implicitamente em um tipo de dados character, se o integer for muito grande para ser ajustado no campo de caractere, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] digitará o caractere ASCII 42, o asterisco (*).
  
As constantes de inteiro maiores que 2.147.483.647 são convertidas no tipo de dados **decimal**, não no tipo de dados **bigint**. O exemplo a seguir mostra que quando o valor limite é excedido, o tipo de dados do resultado é alterado de um **int** para um **decimal**.
  
```sql
SELECT 2147483647 / 2 AS Result1, 2147483649 / 2 AS Result2 ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result1      Result2  
1073741823   1073741824.500000  
```  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir cria uma tabela usando os tipos de dados **bigint**, **int**, **smallint** e **tinyint**. Os valores são inseridos em cada coluna e retornados na instrução SELECT.
  
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
  
## <a name="see-also"></a>Confira também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
