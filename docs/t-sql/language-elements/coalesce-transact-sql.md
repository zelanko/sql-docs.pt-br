---
title: COALESCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COALESCE
- COALESCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], nonnull
- COALESCE function
- first nonnull expressions [SQL Server]
- nonnull expressions
ms.assetid: fafc0dba-f8a8-4aad-9b7f-908e34b74d88
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7360a1927ce460c96c127d6a4f2d5d59668337e0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="coalesce-transact-sql"></a>COALESCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Avalia os argumentos na ordem e retorna o valor atual da primeira expressão que não é avaliada como `NULL` inicialmente. Por exemplo, `SELECT COALESCE(NULL, NULL, 'third_value', 'fourth_value');` retorna o terceiro valor porque esse é o primeiro valor que não é nulo. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
COALESCE ( expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o tipo de dados de *expressão* com a maior precedência de tipo de dados. Se todas as expressões forem não anuláveis (nonnullable), o resultado será digitado como nonnullable.  
  
## <a name="remarks"></a>Remarks  
 Se todos os argumentos forem `NULL`, `COALESCE` retornará `NULL`. Pelo menos um dos valores nulos precisa ser do tipo `NULL`.  
  
## <a name="comparing-coalesce-and-case"></a>Comparando COALESCE e CASE  
 A expressão `COALESCE` é um atalho sintático para a expressão `CASE`.  Ou seja, o código `COALESCE`(*expression1*,*...n*) é reescrito pelo otimizador de consulta como a seguinte expressão `CASE`:  
  
 ```sql  
 CASE  
 WHEN (expression1 IS NOT NULL) THEN expression1  
 WHEN (expression2 IS NOT NULL) THEN expression2  
 ...  
 ELSE expressionN  
 END  
 ```  
  
 Isso significa que os valores de entrada (*expression1*, *expression2*, *expressionN*, etc.) são avaliados várias vezes. Além disso, em conformidade com o padrão do SQL, uma expressão de valor que contém uma subconsulta é considerada não determinística e a subconsulta é avaliada duas vezes. Em ambos os casos, resultados diferentes podem ser retornados entre a primeira avaliação e as avaliações subsequentes.  
  
 Por exemplo, quando o código `COALESCE((subquery), 1)` é executado, a subconsulta é avaliada duas vezes. Como resultado, você pode obter resultados diferentes dependendo do nível de isolamento da consulta. Por exemplo, o código pode retornar `NULL` no nível de isolamento `READ COMMITTED` em um ambiente multiusuário. Para assegurar que resultados estáveis sejam retornados, use o nível de isolamento `SNAPSHOT ISOLATION` ou substitua `COALESCE` pela função `ISNULL`. Como alternativa, você pode reescrever a consulta para inserir a subconsulta em uma subseleção, conforme é mostrado no exemplo a seguir:  
  
```sql  
SELECT CASE WHEN x IS NOT NULL THEN x ELSE 1 END  
from  
(  
SELECT (SELECT Nullable FROM Demo WHERE SomeCol = 1) AS x  
) AS T;  
  
```  
  
## <a name="comparing-coalesce-and-isnull"></a>Comparando COALESCE e ISNULL  
 A função `ISNULL` e a expressão `COALESCE` têm uma finalidade semelhante, mas podem ter um comportamento diferente.  
  
1.  Como `ISNULL` é uma função, ela é avaliada apenas uma vez.  Conforme descrito acima, a entrada de valores para a expressão `COALESCE` pode ser avaliada várias vezes.  
  
2.  A determinação de tipo de dados da expressão resultante é diferente. `ISNULL` usa o tipo de dados do primeiro parâmetro, `COALESCE` segue as regras da expressão `CASE` e retorna o tipo de dados de valor com a precedência mais alta.  
  
3.  A nulidade da expressão resultante é diferente para `ISNULL` e `COALESCE`. O valor retornado `ISNULL` é sempre considerado como um valor que não permite valor nulo (supondo que o valor retornado não permita valor nulo), já o `COALESCE` com parâmetros não nulos é considerado `NULL`. Portanto as expressões `ISNULL(NULL, 1)` e `COALESCE(NULL, 1)`, embora equivalentes, têm valores diferentes de nulidade. Isso fará diferença se você estiver usando essas expressões em colunas computadas, criando restrições de chave ou tornando determinístico o valor retornado de um UDF escalar para que ele possa ser indexado como é mostrado no exemplo a seguir:  
  
    ```sql  
    USE tempdb;  
    GO  
    -- This statement fails because the PRIMARY KEY cannot accept NULL values  
    -- and the nullability of the COALESCE expression for col2   
    -- evaluates to NULL.  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0) PRIMARY KEY,   
    col3 AS ISNULL(col1, 0)   
    );   
  
    -- This statement succeeds because the nullability of the   
    -- ISNULL function evaluates AS NOT NULL.  
  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0),   
    col3 AS ISNULL(col1, 0) PRIMARY KEY   
    );  
    ```  
  
4.  As validações de `ISNULL` e de `COALESCE` também são diferentes. Por exemplo, um valor `NULL` para `ISNULL` é convertido em **int**, já para `COALESCE`, você precisa fornecer um tipo de dados.  
  
5.  `ISNULL` usa apenas dois parâmetros enquanto `COALESCE` usa um número variável de parâmetros.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-running-a-simple-example"></a>A. Executando um exemplo simples  
 O exemplo a seguir mostra como `COALESCE` seleciona os dados da primeira coluna que tem um valor não nulo. Este exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
SELECT Name, Class, Color, ProductNumber,  
COALESCE(Class, Color, ProductNumber) AS FirstNotNull  
FROM Production.Product;  
```  
  
### <a name="b-running-a-complex-example"></a>B. Executando um exemplo complexo  
 No exemplo a seguir, a tabela `wages` inclui três colunas que contêm informações sobre o salário anual dos funcionários: valor por hora, salário e comissão. No entanto, um funcionário recebe apenas um tipo de pagamento. Para determinar o valor total pago a todos os funcionários, use a função `COALESCE` para receber apenas o valor não nulo encontrado em `hourly_wage`, `salary` e `commission`.  
  
```sql  
SET NOCOUNT ON;  
GO  
USE tempdb;  
IF OBJECT_ID('dbo.wages') IS NOT NULL  
    DROP TABLE wages;  
GO  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   identity,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
GO  
INSERT dbo.wages (hourly_wage, salary, commission, num_sales)  
VALUES  
    (10.00, NULL, NULL, NULL),  
    (20.00, NULL, NULL, NULL),  
    (30.00, NULL, NULL, NULL),  
    (40.00, NULL, NULL, NULL),  
    (NULL, 10000.00, NULL, NULL),  
    (NULL, 20000.00, NULL, NULL),  
    (NULL, 30000.00, NULL, NULL),  
    (NULL, 40000.00, NULL, NULL),  
    (NULL, NULL, 15000, 3),  
    (NULL, NULL, 25000, 2),  
    (NULL, NULL, 20000, 6),  
    (NULL, NULL, 14000, 4);  
GO  
SET NOCOUNT OFF;  
GO  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS money) AS 'Total Salary'   
FROM dbo.wages  
ORDER BY 'Total Salary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Total Salary  
 ------------  
 10000.00  
 20000.00  
 20800.00  
 30000.00  
 40000.00  
 41600.00  
 45000.00  
 50000.00  
 56000.00  
 62400.00  
 83200.00  
 120000.00  
  
 (12 row(s) affected)
 ```  
  
### <a name="c-simple-example"></a>C: Exemplo simples  
 O exemplo a seguir demonstra como `COALESCE` seleciona os dados da primeira coluna que tem um valor não nulo. Considere para este exemplo que a tabela `Products` contém estes dados:  
  
 ```  
 Name         Color      ProductNumber  
 ------------ ---------- -------------  
 Socks, Mens  NULL       PN1278  
 Socks, Mens  Blue       PN1965  
 NULL         White      PN9876
 ```  
  
 Em seguida, executaremos a seguinte consulta COALESCE:  
  
```sql  
SELECT Name, Color, ProductNumber, COALESCE(Color, ProductNumber) AS FirstNotNull   
FROM Products ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Name         Color      ProductNumber  FirstNotNull  
 ------------ ---------- -------------  ------------  
 Socks, Mens  NULL       PN1278         PN1278  
 Socks, Mens  Blue       PN1965         Blue  
 NULL         White      PN9876         White
 ```  
  
 Observe que na primeira linha, o valor de `FirstNotNull` é `PN1278`, não `Socks, Mens`. Isso ocorre porque a coluna `Name` não foi especificada como um parâmetro para `COALESCE` no exemplo.  
  
### <a name="d-complex-example"></a>D. Exemplo complexo  
 O exemplo a seguir usa `COALESCE` para comparar os valores em três colunas e retornar apenas o valor não nulo encontrado nas colunas.  
  
```sql  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   NULL,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (1, 10.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (2, 20.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (3, 30.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (4, 40.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (5, NULL, 10000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (6, NULL, 20000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (7, NULL, 30000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (8, NULL, 40000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (9, NULL, NULL, 15000, 3);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (10,NULL, NULL, 25000, 2);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (11, NULL, NULL, 20000, 6);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (12, NULL, NULL, 14000, 4);  
  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS decimal(10,2)) AS TotalSalary   
FROM dbo.wages  
ORDER BY TotalSalary;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Total Salary  
 ------------  
 10000.00  
 20000.00  
 20800.00  
 30000.00  
 40000.00  
 41600.00  
 45000.00  
 50000.00  
 56000.00  
 62400.00  
 83200.00  
 120000.00
 ```  
  
## <a name="see-also"></a>Consulte Também  
 [ISNULL &#40;Transact-SQL&#41;](../../t-sql/functions/isnull-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  
