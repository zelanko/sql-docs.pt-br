---
description: tabela (Transact-SQL)
title: table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ad743fc9864207dedcad050428646abf80fa4f59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88311442"
---
# <a name="table-transact-sql"></a>tabela (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

É um tipo de dados especial que pode ser usado para armazenar um conjunto de resultados para processamento posterior. **table** é usada principalmente para o armazenamento temporário de um conjunto de linhas retornadas como o conjunto de resultados de uma função com valor de tabela. Funções e variáveis podem ser declaradas como do tipo **table**. Variáveis **table** podem ser usadas em funções, procedimentos armazenados e lotes. Para declarar variáveis do tipo **table**, use [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
table_type_definition ::=   
    TABLE ( { <column_definition> | <table_constraint> } [ ,...n ] )   
  
<column_definition> ::=   
    column_name scalar_data_type   
    [ COLLATE <collation_definition> ]   
    [ [ DEFAULT constant_expression ] | IDENTITY [ ( seed , increment ) ] ]   
    [ ROWGUIDCOL ]   
    [ column_constraint ] [ ...n ]   
  
 <column_constraint> ::=   
    { [ NULL | NOT NULL ]   
    | [ PRIMARY KEY | UNIQUE ]   
    | CHECK ( logical_expression )   
    }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n ] )  
     | CHECK ( logical_expression )   
     }   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*table_type_definition*  
É o mesmo subconjunto de informações usado para definir uma tabela em CREATE TABLE. A declaração de tabela inclui definições de coluna, nomes, tipos de dados e restrições. Os únicos tipos de restrição permitidos são PRIMARY KEY, UNIQUE KEY e NULL.  
Para obter mais informações sobre a sintaxe, veja [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md), [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md) e [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  
*collation_definition*  
É a ordenação da coluna composta de uma localidade do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e um estilo de comparação, uma localidade do Windows e a notação binária ou uma ordenação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se *collation_definition* não for especificado, a coluna herdará a ordenação do banco de dados atual. Ou se a coluna estiver definida como um tipo CLR (Common Language Runtime) definido pelo usuário, a coluna herdará a ordenação do tipo definido pelo usuário.
  
## <a name="remarks"></a>Comentários  
**table** As variáveis podem ser referenciadas por nome na cláusula FROM de um lote, conforme mostrado no seguinte exemplo:
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
Fora de uma cláusula FROM, as variáveis **table** devem ser referenciadas usando um alias, conforme mostra o exemplo a seguir:
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
Variáveis **table** fornecem os benefícios seguintes para consultas em pequena escala que têm planos de consulta que não são alterados e quando há preocupações de recompilação:
-   Uma variável **table** se comporta como uma variável local. Ela tem um escopo bem definido. Essa variável pode ser usada na função, no procedimento armazenado ou no lote em que ela é declarada.  
     Dentro de seu escopo, uma variável **table** pode ser usada como uma tabela comum. Pode ser aplicada em qualquer lugar em que uma tabela ou expressão de tabela for usada em instruções SELECT, INSERT, UPDATE e DELETE. Porém, **table** não pode ser usada na seguinte instrução:  
  
```sql
SELECT select_list INTO table_variable;
```
  
As variáveis **table** são automaticamente limpas ao término da função, do procedimento armazenado ou do lote em que estão definidas.
  
-   As variáveis **table** usadas em procedimentos armazenados provocam menos recompilações dos procedimentos armazenados do que quando tabelas temporárias são usadas quando não há opções baseadas no custo que afetem o desempenho.  
-   As transações que envolvem variáveis **table** só existem durante uma atualização na variável **table**. Assim, variáveis **table** requerem menos recursos de log e bloqueio.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições
As variáveis **Table** não têm estatísticas de distribuição. Elas não dispararão recompilações. Em muitos casos, o otimizador criará um plano de consulta supondo que a variável de tabela não tenha linhas. Por esse motivo, tenha cuidado ao usar uma variável de tabela se espera um grande número de linhas (cima de 100). Nesse caso, talvez seja melhor usar tabelas temporárias. Para consultas que unem a variável de tabela com outras tabelas, use a dica RECOMPILE, que levará o otimizador a usar a cardinalidade correta para a variável de tabela.
  
Não há suporte para variáveis **table** no modelo de raciocínio baseado no custo do otimizador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, elas não devem ser usadas quando opções baseadas no custo forem necessárias para obter um plano de consulta eficiente. Tabelas temporárias são preferíveis quando opções baseadas no custo são necessárias. Em geral, esse plano inclui consultas com junções, decisões de paralelismo e opções de seleção de índice.
  
As consultas que modificam variáveis **table** não geram planos de execução de consulta paralelos. O desempenho pode ser afetado quando variáveis **table** grandes ou variáveis **table** em consultas complexas forem modificadas. Considere o uso de tabelas temporárias em situações em que as variáveis **table** são modificadas. Para obter mais informações, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md). As consultas que leem variáveis **table** sem modificá-las ainda podem ser colocadas em paralelo.

> [!IMPORTANT]
> O nível de compatibilidade do banco de dados 150 melhora o desempenho das variáveis de tabela com a introdução da **compilação adiada da variável de tabela**.  Para saber mais, veja [Compilação adiada de variável da tabela](../../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation).
>
  
Índices não podem ser criados explicitamente em variáveis **table** e nenhuma estatística é mantida em variáveis **table**. A partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], uma nova sintaxe foi introduzida, a qual permite que você crie determinados tipos de índice em linha com a definição da tabela.  Usando essa nova sintaxe, você pode criar índices em variáveis de **tabela** como parte da definição de tabela. Em alguns casos, o desempenho pode melhorar com o uso de tabelas temporárias em vez disso, que fornecem suporte de índice completo e estatísticas. Para saber mais sobre tabelas temporárias e criação de índice embutido, confira [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).

Restrições CHECK, valores DEFAULT e colunas computadas na declaração de tipo **table** não podem chamar funções definidas pelo usuário.
  
Não é dado suporte à operação de atribuição entre variáveis **table**.
  
Como as variáveis **table** têm escopo limitado e não fazem parte do banco de dados persistente, elas não são afetadas por reversões de transações.
  
As variáveis table não podem ser alteradas após a criação.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-declaring-a-variable-of-type-table"></a>a. Declarando uma variável de tabela de tipos  
O exemplo a seguir cria uma variável `table` que armazena os valores especificados na cláusula OUTPUT da instrução UPDATE. Seguem duas instruções `SELECT` que retornam os valores em `@MyTableVar` e os resultados da operação de atualização na tabela `Employee`. Os resultados na coluna `INSERTED.ModifiedDate` são diferentes dos valores da coluna `ModifiedDate` na tabela `Employee`. Essa diferença é devido ao gatilho `AFTER UPDATE`, que atualiza o valor de `ModifiedDate` com a data atual, e está definido na tabela `Employee`. Porém, as colunas retornadas de `OUTPUT` refletem os dados antes de os gatilhos serem disparados. Para obter mais informações, confira [Cláusula OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).
  
```sql
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25   
OUTPUT INSERTED.BusinessEntityID,  
       DELETED.VacationHours,  
       INSERTED.VacationHours,  
       INSERTED.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
--Note that ModifiedDate reflects the value generated by an  
--AFTER UPDATE trigger.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. Criando uma função com valor de tabela embutida  
O exemplo a seguir retorna uma função com valor de tabela embutida. Ela retorna três colunas `ProductID`, `Name` e a agregação dos totais acumulados no ano por loja como `YTD Total` para cada produto vendido para a loja.
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```  
  
Para invocar a função, execute esta consulta.
  
```sql
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
## <a name="see-also"></a>Confira também
[COLLATE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
[Funções definidas pelo usuário](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[Usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[Query Hints &#40;Transact-SQL&#41; [Dicas de consulta (Transact-SQL)]](../../t-sql/queries/hints-transact-sql-query.md)
