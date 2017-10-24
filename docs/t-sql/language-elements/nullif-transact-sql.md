---
title: NULLIF (Transact-SQL) | Microsoft Docs
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
- NULLIF
- NULLIF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], equivalent expressions
- expressions [SQL Server], null values
- NULLIF function
- equivalent expressions [SQL Server]
ms.assetid: 44c7b67e-74c7-4bb9-93a4-7a3016bd2feb
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fe8e4663688ce510d9600ebeba9d3c30703ee3aa
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="nullif-transact-sql"></a>NULLIF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna um valor nulo se as duas expressões especificadas forem iguais. Por exemplo, `SELECT NULLIF(4,4) AS Same, NULLIF(5,7) AS Different;` retorna NULL para a primeira coluna (4 e 4), pois os dois valores de entrada são os mesmos. A segunda coluna retorna o primeiro valor (5), porque os dois valores de entrada são diferentes. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
NULLIF ( expression , expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É qualquer escalar válida [expressão](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o mesmo tipo que a primeira *expressão*.  
  
 NULLIF retornará a primeira *expressão* se as duas expressões não forem iguais. Se as expressões forem iguais, NULLIF retornará um valor nulo do tipo do primeiro *expressão*.  
  
## <a name="remarks"></a>Comentários  
 NULLIF é equivalente a uma expressão CASE pesquisada em que as duas expressões são iguais e a expressão resultante é NULL.  
  
 É recomendável não usar funções dependentes de tempo, como RAND(), dentro de uma função NULLIF. Isso pode causar a função a ser avaliada duas vezes e retornar resultados diferentes nas duas invocações.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-budget-amounts-that-have-not-changed"></a>A. Retornando valores de orçamento que não foram alterados  
 O exemplo a seguir cria uma tabela `budgets` para mostrar a um departamento (`dept`) seu orçamento atual (`current_year`) e seu orçamento anterior (`previous_year`). Para o ano atual, `NULL` é usado para departamentos com orçamentos que não foram alterados em relação ao ano anterior, e `0` é usado para orçamentos que ainda não foram determinados. Para descobrir a média somente dos departamentos que receberam um orçamento e para incluir o valor do orçamento do ano anterior (use o valor `previous_year`, em que o `current_year` é `NULL`), combine as funções `NULLIF` e `COALESCE`.  
  
```sql  
CREATE TABLE dbo.budgets  
(  
   dept            tinyint   IDENTITY,  
   current_year      decimal   NULL,  
   previous_year   decimal   NULL  
);  
INSERT budgets VALUES(100000, 150000);  
INSERT budgets VALUES(NULL, 300000);  
INSERT budgets VALUES(0, 100000);  
INSERT budgets VALUES(NULL, 150000);  
INSERT budgets VALUES(300000, 250000);  
GO    
SET NOCOUNT OFF;  
SELECT AVG(NULLIF(COALESCE(current_year,  
   previous_year), 0.00)) AS 'Average Budget'  
FROM budgets;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Average Budget  
 --------------  
 212500.000000  
 (1 row(s) affected)
 ```  
  
### <a name="b-comparing-nullif-and-case"></a>B. Comparando NULLIF e CASE  
 Para mostrar a semelhança entre `NULLIF` e `CASE`, as consultas a seguir avaliam se os valores das colunas `MakeFlag` e `FinishedGoodsFlag` são os mesmos. A primeira consulta usa `NULLIF`. A segunda consulta usa a expressão `CASE`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT ProductID, MakeFlag, FinishedGoodsFlag,   
   NULLIF(MakeFlag,FinishedGoodsFlag)AS 'Null if Equal'  
FROM Production.Product  
WHERE ProductID < 10;  
GO  
  
SELECT ProductID, MakeFlag, FinishedGoodsFlag,'Null if Equal' =  
   CASE  
       WHEN MakeFlag = FinishedGoodsFlag THEN NULL  
       ELSE MakeFlag  
   END  
FROM Production.Product  
WHERE ProductID < 10;  
GO  
```  

### <a name="c-returning-budget-amounts-that-contain-no-data"></a>C: retornando valores de orçamento que não contêm dados  
 O exemplo a seguir cria um `budgets` carrega dados de tabela e usa `NULLIF` para retornar um valor nulo se nenhuma `current_year` nem `previous_year` contém dados.  
  
```sql  
CREATE TABLE budgets (  
   dept           tinyint,  
   current_year   decimal(10,2),  
   previous_year  decimal(10,2)  
);  
  
INSERT INTO budgets VALUES(1, 100000, 150000);  
INSERT INTO budgets VALUES(2, NULL, 300000);  
INSERT INTO budgets VALUES(3, 0, 100000);  
INSERT INTO budgets VALUES(4, NULL, 150000);  
INSERT INTO budgets VALUES(5, 300000, 300000);  
  
SELECT dept, NULLIF(current_year,  
   previous_year) AS LastBudget  
FROM budgets;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 dept   LastBudget  
 ----   -----------  
 1      100000.00  
 2      null 
 3      0.00  
 4      null  
 5      null
 ```  
  
## <a name="see-also"></a>Consulte também  
 [Caso &#40; Transact-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [decimal e numeric &#40; Transact-SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [Funções do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  


