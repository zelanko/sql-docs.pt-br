---
title: "UNIÃO (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COALESCE
- COALESCE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- expressions [SQL Server], nonnull
- COALESCE function
- first nonnull expressions [SQL Server]
- nonnull expressions
ms.assetid: fafc0dba-f8a8-4aad-9b7f-908e34b74d88
caps.latest.revision: "52"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f9cb11cb46ab14ab7b1efee597371799882f0e55
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="coalesce-transact-sql"></a>COALESCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Avalia os argumentos na ordem e retorna o valor atual da primeira expressão que inicialmente não é avaliada como `NULL`. Por exemplo, `SELECT COALESCE(NULL, NULL, 'third_value', 'fourth_value');` retorna o terceiro valor como o terceiro valor é o primeiro valor que não seja nulo. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
COALESCE ( expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *expressão*  
 É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o tipo de dados de *expressão* com maior precedência de tipo de dados. Se todas as expressões forem não anuláveis (nonnullable), o resultado será digitado como nonnullable.  
  
## <a name="remarks"></a>Comentários  
 Se todos os argumentos forem `NULL`, `COALESCE` retorna `NULL`. Pelo menos um dos valores nulos deve ser um tipo `NULL`.  
  
## <a name="comparing-coalesce-and-case"></a>Comparando COALESCE e CASE  
 O `COALESCE` expressão é um atalho sintático para a `CASE` expressão.  Ou seja, o código `COALESCE`(*expression1*,*... n*) é recriado pelo otimizador de consulta como o seguinte `CASE` expressão:  
  
 ```sql  
 CASE  
 WHEN (expression1 IS NOT NULL) THEN expression1  
 WHEN (expression2 IS NOT NULL) THEN expression2  
 ...  
 ELSE expressionN  
 END  
 ```  
  
 Isso significa que os valores de entrada (*expression1*, *expression2*, *expressão*, etc.) são avaliados várias vezes. Além disso, em conformidade com o padrão do SQL, uma expressão de valor que contém uma subconsulta é considerada não determinística e a subconsulta é avaliada duas vezes. Em ambos os casos, resultados diferentes podem ser retornados entre a primeira avaliação e as avaliações subsequentes.  
  
 Por exemplo, quando o código `COALESCE((subquery), 1)` é executado, a subconsulta é avaliada duas vezes. Como resultado, você pode obter resultados diferentes dependendo do nível de isolamento da consulta. Por exemplo, o código pode retornar `NULL` sob o `READ COMMITTED` nível de isolamento em um ambiente multiusuário. Para assegurar resultados estáveis sejam retornados, use o `SNAPSHOT ISOLATION` nível de isolamento ou substitua `COALESCE` com o `ISNULL` função. Como alternativa, você pode reescrever a consulta para inserir a subconsulta em uma Subseleção, conforme mostrado no exemplo a seguir:  
  
```sql  
SELECT CASE WHEN x IS NOT NULL THEN x ELSE 1 END  
from  
(  
SELECT (SELECT Nullable FROM Demo WHERE SomeCol = 1) AS x  
) AS T;  
  
```  
  
## <a name="comparing-coalesce-and-isnull"></a>Comparando COALESCE e ISNULL  
 O `ISNULL` função e o `COALESCE` expressão têm uma finalidade semelhante, mas pode ter um comportamento diferente.  
  
1.  Porque `ISNULL` é uma função, ela é avaliada apenas uma vez.  Conforme descrito acima, a entrada de valores para o `COALESCE` expressão pode ser avaliada várias vezes.  
  
2.  A determinação de tipo de dados da expressão resultante é diferente. `ISNULL`usa o tipo de dados do primeiro parâmetro, `COALESCE` segue o `CASE` expressão regras e retorna o tipo de dados de valor com a precedência mais alta.  
  
3.  A nulidade da expressão resultante é diferente para `ISNULL` e `COALESCE`. O `ISNULL` retornar o valor é sempre considerado não anulável (supondo que o valor de retorno é não nulo) enquanto `COALESCE` com parâmetros não nulos é considerado como `NULL`. Portanto as expressões `ISNULL(NULL, 1)` e `COALESCE(NULL, 1)`, embora equivalentes, têm valores diferentes de nulidade. Isso fará diferença se você estiver usando essas expressões em colunas computadas, criação de restrições de chave ou tornando o valor de retorno de uma UDF escalar determinista para que possa ser indexado como mostrado no exemplo a seguir:  
  
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
  
4.  Validações de `ISNULL` e `COALESCE` também são diferentes. Por exemplo, um `NULL` valor para `ISNULL` é convertido em **int** enquanto para `COALESCE`, você deve fornecer um tipo de dados.  
  
5.  `ISNULL`usa apenas dois parâmetros enquanto `COALESCE` usa um número variável de parâmetros.  
  
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
  
### <a name="c-simple-example"></a>C: exemplo simples de  
 O exemplo a seguir demonstra como `COALESCE` seleciona os dados da primeira coluna que tem um valor não nulo. Suponha para este exemplo que o `Products` tabela contém dados:  
  
 ```  
 Name         Color      ProductNumber  
 ------------ ---------- -------------  
 Socks, Mens  NULL       PN1278  
 Socks, Mens  Blue       PN1965  
 NULL         White      PN9876
 ```  
  
 Em seguida, executarmos a ADESÃO a seguinte consulta:  
  
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
  
 Observe que na primeira linha, o `FirstNotNull` valor é `PN1278`, não `Socks, Mens`. Isso ocorre porque o `Name` coluna não foi especificada como um parâmetro para `COALESCE` no exemplo.  
  
### <a name="d-complex-example"></a>Unidade d: exemplo complexo  
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
  
## <a name="see-also"></a>Consulte também  
 [ISNULL &#40; Transact-SQL &#41;](../../t-sql/functions/isnull-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  
