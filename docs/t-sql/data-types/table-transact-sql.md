---
title: tabela (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 90f8db8df144113d47543ff50c321baed61fba37
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="table-transact-sql"></a>tabela (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

É um tipo de dados especial que pode ser usado para armazenar um conjunto de resultados para processamento posterior. **tabela** é usado principalmente para armazenamento temporário de um conjunto de linhas retornadas como o conjunto de resultados de uma função com valor de tabela. Funções e variáveis podem ser declarados como sendo do tipo **tabela**. **tabela** variáveis podem ser usadas em funções, procedimentos armazenados e lotes. Para declarar variáveis do tipo **tabela**, use [DECLARE @local_variable ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
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
  
## <a name="arguments"></a>Argumentos  
*table_type_definition*  
É o mesmo subconjunto de informações usado para definir uma tabela em CREATE TABLE. A declaração de tabela inclui definições de coluna, nomes, tipos de dados e restrições. Os únicos tipos de restrição permitidos são PRIMARY KEY, UNIQUE KEY e NULL.  
Para obter mais informações sobre a sintaxe, consulte [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md), [Criar função &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md), e [DECLARE @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  
*collation_definition*  
É o agrupamento da coluna que é composto de um [!INCLUDE[msCoName](../../includes/msconame-md.md)] localidade do Windows e um estilo de comparação, uma localidade do Windows e a notação binária ou um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agrupamento. Se *collation_definition* não for especificado, a coluna herdará o agrupamento do banco de dados atual. Ou se a coluna estiver definida como um tipo CLR (Common Language Runtime) definido pelo usuário, a coluna herdará o agrupamento do tipo definido pelo usuário.
  
## <a name="remarks"></a>Comentários  
**tabela** variáveis podem ser referenciadas por nome na cláusula FROM de um lote, conforme mostrado no exemplo a seguir:
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
Fora de uma cláusula FROM, **tabela** variáveis devem ser referenciadas por meio de um alias, conforme mostrado no exemplo a seguir:
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
**tabela** variáveis fornecem os seguintes benefícios para consultas em pequena escala com planos de consulta que não são alterados e quando há preocupações de recompilação:
-   Um **tabela** variável se comporta como uma variável local. Ela tem um escopo bem definido. Ela é a função, o procedimento armazenado ou o lote em que está declarada.  
     Dentro de seu escopo, um **tabela** variável pode ser usada como uma tabela comum. Pode ser aplicada em qualquer lugar em que uma tabela ou expressão de tabela for usada em instruções SELECT, INSERT, UPDATE e DELETE. No entanto, **tabela** não pode ser usado na instrução a seguir:  
  
```sql
SELECT select_list INTO table_variable;
```
  
**tabela** variáveis são automaticamente limpos no final de função, procedimento armazenado ou lote no qual eles são definidos.
  
-   **tabela** variáveis usadas em procedimentos armazenados causam menos recompilações dos procedimentos armazenados que quando tabelas temporárias são usadas quando não houver nenhuma opção baseado no custo que afetam o desempenho.  
-   As transações que envolvem **tabela** variáveis última apenas para a duração de uma atualização no **tabela** variável. Portanto, **tabela** variáveis exigem menos recursos de log e bloqueio.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições
**Tabela** variáveis não tem estatísticas de distribuição, elas não dispararão recompilações. Portanto, em muitos casos, o otimizador criará um plano de consulta supondo que a variável de tabela não tem linhas Por esse motivo, tenha cuidado ao usar uma variável de tabela se espera um grande número de linhas (cima de 100). Nesse caso, talvez seja melhor usar tabelas temporárias. Como alternativa, para consultas que unem a variável de tabela com outras tabelas, use a dica RECOMPILE, o que fará com que o otimizador a usar a cardinalidade correta para a variável de tabela.
  
**tabela** variáveis não têm suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modelo de raciocínio baseado no custo do otimizador. Portanto, elas não devem ser usadas quando opções baseadas no custo são necessárias para obter um plano de consulta eficiente. Tabelas temporárias são preferíveis quando opções baseadas no custo são necessárias. Em geral, isso inclui consultas com junções, decisões de paralelismo e opções de seleção de índice.
  
Consultas que modificam **tabela** variáveis não geram planos de execução de consulta paralela. Desempenho pode ser afetado quando grandes **tabela** variáveis, ou **tabela** variáveis em consultas complexas, são modificadas. Nessas situações, considere o uso de tabelas temporárias em seu lugar. Para obter mais informações, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md). As consultas que leem **tabela** ainda podem ser paralelizadas variáveis sem modificá-las.
  
Índices não podem ser criados explicitamente sobre **tabela** variáveis e nenhuma estatística é mantidas em **tabela** variáveis. Em alguns casos, o desempenho pode melhorar com o uso de tabelas temporárias em seu lugar, as quais oferecem suporte a índices e estatísticas. Para obter mais informações sobre tabelas temporárias, consulte [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).
  
Verificar restrições, valores padrão e colunas computadas no **tabela** declaração de tipo não é possível chamar funções definidas pelo usuário.
  
Operação de atribuição entre **tabela** não há suporte para variáveis.
  
Porque **tabela** variáveis têm escopo limitado e não fazem parte do banco de dados persistente, elas não são afetadas por reversões de transação.
  
As variáveis de tabela não podem ser alteradas após a criação.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-declaring-a-variable-of-type-table"></a>A. Declarando uma variável de tabela de tipos  
O exemplo a seguir cria uma variável `table` que armazena os valores especificados na cláusula OUTPUT da instrução UPDATE. Seguem duas instruções `SELECT` que retornam os valores em `@MyTableVar` e os resultados da operação de atualização na tabela `Employee`. Observe que os resultados no `INSERTED.ModifiedDate` coluna diferentes dos valores no `ModifiedDate` coluna o `Employee` tabela. Isso porque o gatilho `AFTER UPDATE`, que atualiza o valor de `ModifiedDate` com a data atual, está definido na tabela `Employee`. Porém, as colunas retornadas de `OUTPUT` refletem os dados antes de os gatilhos serem disparados. Para obter mais informações, consulte [cláusula OUTPUT &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).
  
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
  
## <a name="see-also"></a>Consulte também
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
[Funções definidas pelo usuário](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[Usar com valor de tabela parâmetros &#40; mecanismo de banco de dados &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[Query Hints &#40;Transact-SQL&#41; [Dicas de consulta (Transact-SQL)]](../../t-sql/queries/hints-transact-sql-query.md)
  
  
