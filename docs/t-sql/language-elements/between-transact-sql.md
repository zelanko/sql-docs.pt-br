---
title: BETWEEN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BETWEEN
- BETWEEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- inclusive ranges
- testing range
- exclusive ranges
- NOT BETWEEN operator
- BETWEEN operator
- range to test [SQL Server]
ms.assetid: a5d5b050-203e-4355-ac85-e08ef5ca7823
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 269aaf6d7c5f0b628a7750a5113ca111e09fc84b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43063713"
---
# <a name="between-transact-sql"></a>BETWEEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica um intervalo a ser testado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
test_expression [ NOT ] BETWEEN begin_expression AND end_expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *test_expression*  
 É a [expressão](../../t-sql/language-elements/expressions-transact-sql.md) a ser testada no intervalo definido por *begin_expression* e *end_expression*. *test_expression* precisa ser do mesmo tipo de dados que *begin_expression* e *end_expression*.  
  
 NOT  
 Especifica que o resultado do predicado deve ser negado.  
  
 *begin_expression*  
 É qualquer expressão válida. *begin_expression* precisa ser do mesmo tipo de dados que *test_expression* e *end_expression*.  
  
 *end_expression*  
 É qualquer expressão válida. *end_expression* precisa ser do mesmo tipo de dados que *test_expression* e *begin_expression*.  
  
 AND  
 Atua como um espaço reservado que indica se *test_expression* deve estar dentro do intervalo indicado por *begin_expression* e *end_expression*.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Booliano**  
  
## <a name="result-value"></a>Valor do resultado  
 BETWEEN retornará **TRUE** se o valor de *test_expression* for maior ou igual ao valor de *begin_expression* e menor ou igual ao valor de *end_expression*.  
  
 NOT BETWEEN retornará **TRUE** se o valor de *test_expression* for menor que o valor de *begin_expression* ou maior que o valor de *end_expression* .  
  
## <a name="remarks"></a>Remarks  
 Para especificar um intervalo exclusivo, use os operadores maior que (>) e menor que (<). Se qualquer entrada para o predicado BETWEEN ou NOT BETWEEN for NULL, o resultado será UNKNOWN.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-between"></a>A. Usando BETWEEN  
 O exemplo a seguir retorna informações sobre as funções de banco de dados em um banco de dados. A primeira consulta retorna todas as funções. O segundo exemplo usa a cláusula `BETWEEN` para limitar as funções aos valores `database_id` especificados.  
  
```sql  
SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R';

SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R'
AND principal_id BETWEEN 16385 AND 16390;
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]   
```  
principal_id    name
------------  ---- 
0               public
16384           db_owner
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
16391           db_datawriter
16392           db_denydatareader
16393           db_denydatawriter
```  
```  
principal_id    name
------------  ---- 
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
```  
  
### <a name="b-using--and--instead-of-between"></a>B. Usando > e < em vez de BETWEEN  
 O exemplo a seguir usa os operadores maior que (`>`) e menor que (`<`) e, como esses operadores não são inclusivos, retorna nove linhas em vez das dez retornadas no exemplo anterior.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate > 27 AND ep.Rate < 30  
ORDER BY ep.Rate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 FirstName   LastName             Rate  
 ---------   -------------------  ---------  
 Paula       Barreto de Mattos    27.1394  
 Janaina     Bueno                27.4038  
 Dan         Bacon                27.4038  
 Ramesh      Meyyappan            27.4038  
 Karen       Berg                 27.4038  
 David       Bradley              28.7500  
 Hazem       Abolrous             28.8462  
 Ovidiu      Cracium              28.8462  
 Rob         Walters              29.8462  
 ```    
  
### <a name="c-using-not-between"></a>C. Usando NOT BETWEEN  
 O exemplo a seguir localiza todas as linhas fora de um intervalo especificado de `27` a `30`.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate NOT BETWEEN 27 AND 30  
ORDER BY ep.Rate;  
GO  
```  
  
### <a name="d-using-between-with-datetime-values"></a>D. Usando BETWEEN com valores de data e hora  
 O exemplo a seguir recupera as linhas nas quais os valores de **datetime** estão entre `'20011212'` e `'20020105'`, inclusivo.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, RateChangeDate  
FROM HumanResources.EmployeePayHistory  
WHERE RateChangeDate BETWEEN '20011212' AND '20020105';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 BusinessEntityID RateChangeDate  
 ----------- -----------------------  
 3           2001-12-12 00:00:00.000  
 4           2002-01-05 00:00:00.000  
 ```  
 
 A consulta recupera as linhas esperadas porque os valores de data na consulta e os valores de **datetime** armazenados na coluna `RateChangeDate` foram especificados sem a parte de hora da data. Quando a parte de hora não é especificada, o padrão é 12:00. Observe que uma linha que contém uma parte de hora posterior a 00h00 em 2002-01-05 não será retornada por essa consulta porque está fora do intervalo.  
  
  
## <a name="see-also"></a>Consulte Também  
 [&#62; &#40;Maior que&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/greater-than-transact-sql.md)   
 [&#60; &#40;Menor que&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/less-than-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


