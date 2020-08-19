---
description: Exemplos de SELECT (Transact-SQL)
title: Exemplos de SELECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- parentheses [SQL Server]
- GROUP BY clause, SELECT statement
- query hints [SQL Server]
- ALL keyword
- ROLLUP operator
- SELECT statement [SQL Server], examples
- correlated subqueries, SELECT statement
- SELECT INTO statement
- ORDER BY clause [Transact-SQL]
- GROUPING function
- index hints [SQL Server]
- HAVING clause, SELECT statement
- DISTINCT keyword
- CUBE operator
- UNION operator [SQL Server]
- computed sums
- WHERE clause, SELECT statement
ms.assetid: 9b9caa3d-e7d0-42e1-b60b-a5572142186c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 035210bd3dcba6b8344402d28a3950caa14dbf1b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417052"
---
# <a name="select-examples-transact-sql"></a>Exemplos de SELECT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Este tópico fornece exemplos de uso da instrução [SELECT](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="a-using-select-to-retrieve-rows-and-columns"></a>a. Usando SELECT para recuperar linhas e colunas  
 O exemplo a seguir mostra três exemplos de código. Este primeiro retorna todas as linhas (nenhuma cláusula WHERE foi especificada) e todas as colunas (usando o `*`) da tabela `Product` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
 [!code-sql[Select#SelectExamples1](../../t-sql/queries/codesnippet/tsql/select-examples-transact_1.sql)]  
  
 Este exemplo retorna todas as linhas (nenhuma cláusula WHERE foi especificada) e somente um subconjunto das colunas (`Name`, `ProductNumber`, `ListPrice`) da tabela `Product` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Além disso, um título de coluna é adicionado.  
  
 [!code-sql[Select#SelectExamples2](../../t-sql/queries/codesnippet/tsql/select-examples-transact_2.sql)]  
  
 Este exemplo retorna somente as linhas de `Product` que têm uma linha de produto igual a `R` e que tenham dias para manufatura menores que `4`.  
  
 [!code-sql[Select#SelectExamples3](../../t-sql/queries/codesnippet/tsql/select-examples-transact_3.sql)]  
  
## <a name="b-using-select-with-column-headings-and-calculations"></a>B. Usando SELECT com títulos de coluna e cálculos  
 Os exemplos a seguir retornam todas as linhas da tabela `Product`. O primeiro exemplo retorna o total de vendas e os descontos para cada produto. No segundo exemplo, a receita total é calculada para cada produto.  
  
 [!code-sql[Select#SelectExamples4](../../t-sql/queries/codesnippet/tsql/select-examples-transact_4.sql)]  
  
 Esta é a consulta que calcula a receita para cada produto em cada ordem de vendas.  
  
 [!code-sql[Select#SelectExamples5](../../t-sql/queries/codesnippet/tsql/select-examples-transact_5.sql)]  
  
## <a name="c-using-distinct-with-select"></a>C. Usando DISTINCT com SELECT  
 O exemplo a seguir usa `DISTINCT` para impedir a recuperação de títulos duplicados.  
  
 [!code-sql[Select#SelectExamples6](../../t-sql/queries/codesnippet/tsql/select-examples-transact_6.sql)]  
  
## <a name="d-creating-tables-with-select-into"></a>D. Criando tabelas com SELECT INTO  
 O primeiro exemplo a seguir cria uma tabela temporária denominada `#Bicycles` em `tempdb`.  
  
 [!code-sql[Select#SelectExamples7](../../t-sql/queries/codesnippet/tsql/select-examples-transact_7.sql)]  
  
 Este segundo exemplo cria a tabela permanente `NewProducts`.  
  
 [!code-sql[Select#SelectExamples8](../../t-sql/queries/codesnippet/tsql/select-examples-transact_8.sql)]  
  
## <a name="e-using-correlated-subqueries"></a>E. Usando subconsultas correlacionadas
Uma subconsulta correlacionada é uma consulta que depende da consulta externa para obter os valores. Essa consulta pode ser executada repetidamente, uma vez para cada linha que possa ser selecionada pela consulta externa.

O primeiro exemplo mostra consultas semanticamente equivalentes para ilustrar a diferença entre usar a palavra-chave `EXISTS` e a palavra-chave `IN`. Ambos são exemplos de uma subconsulta válida que recupera uma instância de cada nome de produto para o qual o modelo do produto é uma camisa de marca de manga longa e os números de `ProductModelID` são correspondentes entre as tabelas `Product` e `ProductModel`.  
  
 [!code-sql[Select#SelectExamples9](../../t-sql/queries/codesnippet/tsql/select-examples-transact_9.sql)]  
  
 O próximo exemplo usa `IN` e recupera uma instância do nome e do sobrenome de cada funcionário para os quais o bônus da tabela `SalesPerson` é `5000.00` e para os quais existam números de identificação de funcionário correspondentes nas tabelas `Employee` e `SalesPerson`.  
  
 [!code-sql[Select#SelectExamples10](../../t-sql/queries/codesnippet/tsql/select-examples-transact_10.sql)]  
  
 A subconsulta anterior dessa instrução não pode ser avaliada independentemente da consulta externa. É necessário um valor de `Employee.EmployeeID`, mas esse valor é alterado à medida que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] examina diferentes linhas em `Employee`.  
  
 Uma subconsulta correlata também pode ser usada na cláusula `HAVING` de uma consulta externa. Este exemplo localiza os modelos de produto cujo preço máximo de tabela é mais que o dobro da média para o modelo.  
  
 [!code-sql[Select#SelectExamples11](../../t-sql/queries/codesnippet/tsql/select-examples-transact_11.sql)]  
  
 Este exemplo usa duas subconsultas correlatas para localizar os nomes de funcionários que venderam um produto específico.  
  
 [!code-sql[Select#SelectExamples12](../../t-sql/queries/codesnippet/tsql/select-examples-transact_12.sql)]  
  
## <a name="f-using-group-by"></a>F. Usando GROUP BY  
 O exemplo a seguir localiza o total de cada ordem de vendas no banco de dados.  
  
 [!code-sql[Select#SelectExamples13](../../t-sql/queries/codesnippet/tsql/select-examples-transact_13.sql)]  
  
 Devido à cláusula `GROUP BY`, somente uma linha que contenha a soma de todas as vendas será retornada para cada ordem de vendas.  
  
## <a name="g-using-group-by-with-multiple-groups"></a>G. Usando GROUP BY com vários grupos  
 O exemplo a seguir localiza o preço médio e a soma das vendas do ano até a data atual, agrupadas por ID de produto e ID de oferta especial.  
  
 [!code-sql[Select#SelectExamples14](../../t-sql/queries/codesnippet/tsql/select-examples-transact_14.sql)]  
  
## <a name="h-using-group-by-and-where"></a>H. Usando GROUP BY e WHERE  
 O exemplo a seguir põe os resultados em grupos depois de recuperar apenas as linhas com preços de tabela maiores que `$1000`.  
  
 [!code-sql[Select#SelectExamples15](../../t-sql/queries/codesnippet/tsql/select-examples-transact_15.sql)]  
  
## <a name="i-using-group-by-with-an-expression"></a>I. Usando GROUP BY com uma expressão  
 O exemplo a seguir agrupa por uma expressão. É possível agrupar por uma expressão se a mesma não contiver funções de agregação.  
  
 [!code-sql[Select#SelectExamples16](../../t-sql/queries/codesnippet/tsql/select-examples-transact_16.sql)]  
  
## <a name="j-using-group-by-with-order-by"></a>J. Usando GROUP BY com ORDER BY  
 O exemplo a seguir localiza o preço médio de cada tipo de produto e ordena os resultados por preço médio.  
  
 [!code-sql[Select#SelectExamples18](../../t-sql/queries/codesnippet/tsql/select-examples-transact_17.sql)]  
  
## <a name="k-using-the-having-clause"></a>K. Usando a cláusula HAVING  
 O primeiro exemplo a seguir mostra uma cláusula `HAVING` com uma função de agregação. Ela agrupa as linhas da tabela `SalesOrderDetail` por ID de produto e elimina os produtos cujas quantidades médias de pedido forem cinco ou menos. O segundo exemplo mostra uma cláusula `HAVING` sem funções de agregação.  
  
 [!code-sql[Select#SelectExamples19](../../t-sql/queries/codesnippet/tsql/select-examples-transact_18.sql)]  
  
 Esta consulta usa a cláusula `LIKE` na cláusula `HAVING`.  
  
```sql
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, CarrierTrackingNumber   
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID, CarrierTrackingNumber  
HAVING CarrierTrackingNumber LIKE '4BD%'  
ORDER BY SalesOrderID ;  
GO  
```  
  
## <a name="l-using-having-and-group-by"></a>L. Usando HAVING e GROUP BY  
 O exemplo a seguir mostra o uso de cláusulas `GROUP BY`, `HAVING`, `WHERE` e `ORDER BY` em uma instrução `SELECT`. Ele produz grupos e valores resumidos, mas o faz depois de eliminar os produtos com preços acima de $25 e quantidades médias de pedido abaixo de 5. Também organiza os resultados por `ProductID`.  
  
 [!code-sql[Select#SelectExamples21](../../t-sql/queries/codesnippet/tsql/select-examples-transact_19.sql)]  
  
## <a name="m-using-having-with-sum-and-avg"></a>M. Usando HAVING com SUM e AVG  
 O exemplo a seguir agrupa a tabela `SalesOrderDetail` por ID de produto e somente inclui os grupos de produtos que têm pedidos totalizando mais de `$1000000.00` e cujas quantidades médias do pedido são inferiores a `3`.  
  
 [!code-sql[Select#SelectExamples22](../../t-sql/queries/codesnippet/tsql/select-examples-transact_20.sql)]  
  
 Para consultar os produtos que tiveram vendas totais maiores que `$2000000.00`, use esta consulta:  
  
 [!code-sql[Select#SelectExamples23](../../t-sql/queries/codesnippet/tsql/select-examples-transact_21.sql)]  
  
 Para certificar-se de que existam pelo menos mil e quinhentos itens envolvidos nos cálculos para cada produto, use `HAVING COUNT(*) > 1500` para eliminar os produtos que retornam totais para menos que `1500` itens vendidos. A consulta tem esta aparência:  
  
 [!code-sql[Select#SelectExamples24](../../t-sql/queries/codesnippet/tsql/select-examples-transact_22.sql)]  
  
## <a name="n-using-the-index-optimizer-hint"></a>N. Usando a dica de otimização INDEX  
 O exemplo a seguir mostra dois modos de uso da dica de otimização `INDEX`. O primeiro exemplo mostra como forçar o otimizador a usar um índice não clusterizado para recuperar linhas de uma tabela e o segundo exemplo força uma verificação da tabela usando um índice 0.  
  
 [!code-sql[Select#SelectExamples45](../../t-sql/queries/codesnippet/tsql/select-examples-transact_23.sql)]  
  
## <a name="m-using-option-and-the-group-hints"></a>M. Usando OPTION e as dicas de GROUP  
 O exemplo a seguir mostra como a cláusula `OPTION (GROUP)` é usada com uma cláusula `GROUP BY`.  
  
 [!code-sql[Select#SelectExamples46](../../t-sql/queries/codesnippet/tsql/select-examples-transact_24.sql)]  
  
## <a name="o-using-the-union-query-hint"></a>O. Usando a dica de consulta UNION  
 O exemplo a seguir usa a dica de consulta `MERGE UNION`.  
  
 [!code-sql[Select#SelectExamples47](../../t-sql/queries/codesnippet/tsql/select-examples-transact_25.sql)]  
  
## <a name="p-using-a-simple-union"></a>P. Usando uma UNION simples  
 No exemplo a seguir, o conjunto de resultados inclui o conteúdo das colunas `ProductModelID` e `Name` das tabelas `ProductModel` e `Gloves`.  
  
 [!code-sql[Select#SelectExamples48](../../t-sql/queries/codesnippet/tsql/select-examples-transact_26.sql)]  
  
## <a name="q-using-select-into-with-union"></a>Q. Usando SELECT INTO com UNION  
 No exemplo a seguir, a cláusula `INTO` da segunda instrução `SELECT` especifica que a tabela denominada `ProductResults` contenha o conjunto de resultados final da união das colunas designadas das tabelas `ProductModel` e `Gloves`. Observe que a tabela `Gloves` é criada na primeira instrução `SELECT`.  
  
 [!code-sql[Select#SelectExamples49](../../t-sql/queries/codesnippet/tsql/select-examples-transact_27.sql)]  
  
## <a name="r-using-union-of-two-select-statements-with-order-by"></a>R. Usando UNION de duas instruções SELECT com ORDER BY  
 A ordem de determinados parâmetros usados com a cláusula UNION é importante. O exemplo a seguir mostra o uso incorreto e correto de `UNION` em duas instruções `SELECT` nas quais uma coluna deve ser renomeada na saída.  
  
 [!code-sql[Select#SelectExamples50](../../t-sql/queries/codesnippet/tsql/select-examples-transact_28.sql)]  
  
## <a name="s-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>S. Usando UNION de três instruções SELECT para mostrar os efeitos de ALL e parênteses  
 Os exemplos a seguir usam `UNION` para combinar os resultados de três tabelas que têm as mesmas 5 linhas de dados. O primeiro exemplo usa `UNION ALL` para mostrar os registros duplicados e retorna todas as 15 linhas. O segundo exemplo usa `UNION` sem `ALL` para eliminar as linhas duplicadas dos resultados combinados das três instruções `SELECT` e retorna 5 linhas.  
  
 O terceiro exemplo usa `ALL` com a primeira `UNION` e parênteses cercam a segunda `UNION` que não está usando `ALL`. A segunda `UNION` é processada em primeiro lugar porque está entre parênteses e retorna 5 linhas porque a opção `ALL` não é usada e as linhas duplicadas são removidas. Essas 5 linhas são combinadas com os resultados do primeiro `SELECT` usando as palavras-chave `UNION ALL`. Isso não remove as duplicatas entre os dois conjuntos de cinco linhas. O resultado final tem 10 linhas.  
  
 [!code-sql[Select#SelectExamples51](../../t-sql/queries/codesnippet/tsql/select-examples-transact_29.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [UNION &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-union-transact-sql.md)   
 [EXCEPT e INTERSECT &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [PathName &#40;Transact-SQL&#41;](../../relational-databases/system-functions/pathname-transact-sql.md)   
 [Cláusula INTO &#40;Transact-SQL&#41;](../../t-sql/queries/select-into-clause-transact-sql.md)  
  
  
