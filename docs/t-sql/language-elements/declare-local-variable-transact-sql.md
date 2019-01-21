---
title: DECLARE @local_variable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECLARE
- DECLARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table-valued parameters
- variables [SQL Server], declaring
- DECLARE statement
- declaring variables
ms.assetid: d1635ebb-f751-4de1-8bbc-cae161f90821
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cfe135d53fafa22df7d967f495a7bcfd87dbb2f7
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54299973"
---
# <a name="declare-localvariable-transact-sql"></a>DECLARE @local_variable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  > [!div class="nextstepaction"]
  > [Compartilhe seus comentários sobre o Sumário do SQL Docs!](https://aka.ms/sqldocsurvey)

  As variáveis são declaradas no corpo de um lote ou procedimento com a instrução DECLARE e valores são atribuídos com uma instrução SET ou SELECT. As variáveis de cursor podem ser declaradas com essa instrução e usadas com outras instruções relacionadas ao cursor. Depois da declaração, todas as variáveis são inicializadas como NULL, a menos que um valor seja fornecido como parte da declaração.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DECLARE   
{   
    { @local_variable [AS] data_type  [ = value ] }  
  | { @cursor_variable_name CURSOR }  
} [,...n]   
| { @table_variable_name [AS] <table_type_definition> }   
  
<table_type_definition> ::=   
     TABLE ( { <column_definition> | <table_constraint> } [ ,...n] )   
  
<column_definition> ::=   
     column_name { scalar_data_type | AS computed_column_expression }  
     [ COLLATE collation_name ]   
     [ [ DEFAULT constant_expression ] | IDENTITY [ (seed ,increment ) ] ]   
     [ ROWGUIDCOL ]   
     [ <column_constraint> ]   
  
<column_constraint> ::=   
     { [ NULL | NOT NULL ]   
     | [ PRIMARY KEY | UNIQUE ]   
     | CHECK ( logical_expression )   
     | WITH ( <index_option > )  
     }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n] )   
     | CHECK ( search_condition )   
     }   
  
<index_option> ::=  
See CREATE TABLE for index option syntax.  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DECLARE   
{{ @local_variable [AS] data_type } [ =value [ COLLATE <collation_name> ] ] } [,...n]  
  
```  
  
## <a name="arguments"></a>Argumentos  
@*local_variable*  
 É o nome de uma variável. Os nomes de variável devem começar com uma arroba (@). Os nomes de variável local devem obedecer às regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
*data_type*  
 É qualquer tipo de tabela CLR (Common Language Runtime) definido pelo usuário e fornecido pelo sistema ou tipo de dados alias. Uma variável não pode ser de um tipo de dados **text**, **ntext** ou **image**.  
  
 Para obter mais informações sobre tipos de dados do sistema, consulte [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md). Para obter mais informações sobre tipos de dados CLR definidos pelo usuário ou tipos de dados alias, consulte [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md).  
  
 =*value*  
 Atribui um valor à variável embutida. O valor pode ser uma constante ou uma expressão, mas deve corresponder ao tipo de declaração de variável ou ser convertido implicitamente nesse tipo. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
@*cursor_variable_name*  
 É o nome de uma variável de cursor. Os nomes de variável de cursor devem começar com uma arroba (@) e devem ser compatíveis com as regras para identificadores.  
  
CURSOR  
 Especifica que a variável é uma variável de cursor local.  
  
@*table_variable_name*  
 É o nome de uma variável do tipo **table**. Os nomes de variável devem começar com uma arroba (@) e devem ser compatíveis com as regras para identificadores.  
  
<table_type_definition>  
Define o tipo de dados **table**. A declaração de tabela inclui definições de coluna, nomes, tipos de dados e restrições. Os únicos tipos de restrição permitidos são PRIMARY KEY, UNIQUE, NULL e CHECK. Um tipo de dados alias não pode ser usado como um tipo de dados escalar de coluna se uma regra ou definição padrão for associada ao tipo.
  
\<table_type_definiton> É um subconjunto de informações usado para definir uma tabela em CREATE TABLE. Elementos e definições essenciais são incluídos aqui. Para obter mais informações, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 *n*  
 É um espaço reservado que indica que várias variáveis podem ser especificadas e valores podem ser atribuídos. Ao declarar variáveis **table**, a variável **table** deve ser a única declarada na instrução DECLARE.  
  
 *column_name*  
 É o nome da coluna na tabela.  
  
 *scalar_data_type*  
 Especifica que a coluna é um tipo de dados escalar.  
  
 *computed_column_expression*  
 É uma expressão que define o valor de uma coluna computada. Essa coluna é computada a partir de uma expressão que usa outras colunas na mesma tabela. Por exemplo, uma coluna computada pode ter a definição **cost** AS **price \* qty**. A expressão pode ser o nome de uma coluna não computada, constante, função interna, variável ou qualquer combinação dessas, conectada por um ou mais operadores. A expressão não pode ser uma subconsulta ou uma função definida pelo usuário. A expressão não pode fazer referência a um tipo de dados CLR definido pelo usuário.  
  
 [ COLLATE *collation_name*]  
 Especifica a ordenação da coluna. *collation_name* pode ser um nome de ordenação do Windows ou um nome de ordenação SQL e é aplicável somente a colunas dos tipos de dados **char**, **varchar**, **text**, **nchar**, **nvarchar** e **ntext**. Se não for especificado, à coluna será atribuída a ordenação do tipo de dados definido pelo usuário (se a coluna for de um tipo de dados definido pelo usuário) ou a ordenação do banco de dados atual.  
  
 Para obter mais informações sobre os nomes de ordenação do Windows e do SQL, veja [COLLATE &#40;Transact-SQL &#41;](~/t-sql/statements/collations.md).  
  
 DEFAULT  
 Especifica o valor fornecido para a coluna quando um valor não for fornecido explicitamente durante uma inserção. As definições de DEFAULT podem ser aplicadas a qualquer coluna, com exceção das definidas como **timestamp** ou das colunas com a propriedade IDENTITY. As definições DEFAULT serão removidas quando a tabela for descartada. Somente um valor constante, como uma cadeia de caracteres, uma função de sistema, como SYSTEM_USER() ou NULL pode ser usado como padrão. Para manter a compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um nome de restrição pode ser atribuído a um DEFAULT.  
  
 *constant_expression*  
 É uma constante, um NULL ou uma função de sistema usada como valor de coluna padrão.  
  
 IDENTITY  
 Indica que a nova coluna é uma coluna de identidade. Quando uma nova linha é adicionada à tabela, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um valor incremental exclusivo para a coluna. As colunas de identidade, em geral, são usadas juntamente com restrições PRIMARY KEY para servir de identificador exclusivo de linha para a tabela. A propriedade IDENTITY pode ser atribuída às colunas **tinyint**, **smallint**, **int**, **decimal(p,0)** ou **numeric(p,0)**. Apenas uma coluna de identidade pode ser criada por tabela. Padrões associados e restrições DEFAULT não podem ser usados com uma coluna de identidade. Você deve especificar a semente e o incremento, ou nenhum dos dois. Se nenhum for especificado, o padrão será (1,1).  
  
 *seed*  
 É o valor usado para a primeira linha carregada na tabela.  
  
 *increment*  
 É o valor incremental adicionado ao valor de identidade da linha anterior que foi carregada.  
  
 ROWGUIDCOL  
 Indica que a nova coluna é uma coluna de identificador exclusivo global de linha. Somente uma coluna **uniqueidentifier** por tabela pode ser designada como a coluna ROWGUIDCOL. A propriedade ROWGUIDCOL pode ser atribuída somente a uma coluna **uniqueidentifier**.  
  
 NULL | NOT NULL  
 Indica se será permitido um valor nulo na variável. O padrão é NULO.  
  
 PRIMARY KEY  
 É uma restrição que impõe a integridade de entidade para uma coluna ou colunas especificadas por meio de um índice exclusivo. Somente uma restrição PRIMARY KEY pode ser criada por tabela.  
  
 UNIQUE  
 É uma restrição que fornece a integridade de entidade para uma coluna ou colunas especificadas por meio de um índice exclusivo. Uma tabela pode ter várias restrições UNIQUE.  
  
 CHECK  
 É uma restrição que impõe a integridade de domínio limitando os possíveis valores que podem ser inseridos em uma ou mais colunas.  
  
 *logical_expression*  
 É uma expressão lógica que retorna TRUE ou FALSE.  
  
## <a name="remarks"></a>Remarks  
 As variáveis geralmente são usadas em um lote ou procedimento como contadores para WHILE, LOOP ou para um bloco IF...ELSE.  
  
 As variáveis podem ser usadas somente em expressões, não no lugar de nomes de objeto ou palavras-chave. Para construir instruções SQL dinâmicas, use EXECUTE.  
  
 O escopo de uma variável local é o lote no qual ela é declarada.  
 
 Uma variável de tabela não é necessariamente residente em memória. Sob demanda de memória, as páginas que pertencem a uma variável de tabela podem ser enviadas para fora do tempdb.
  
 Uma variável de cursor que atualmente tem um cursor atribuído pode ser mencionada como uma fonte em uma:  
  
-   Instrução CLOSE.  
  
-   Instrução DEALLOCATE.  
  
-   Instrução FETCH.  
  
-   Instrução OPEN.  
  
-   Instrução DELETE ou UPDATE posicionada.  
  
-   Instrução de variável SET CURSOR (à direita).  
  
 Em todas essas instruções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um erro se uma variável de cursor mencionada existir, mas não tiver no cursor alocado atualmente. Se uma variável de cursor mencionada não existir, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará o mesmo erro ocorrido para uma variável não declarada de outro tipo.  
  
 Uma variável de cursor:  
  
-   Pode ser o destino de um tipo de cursor ou de outra variável de cursor. Para obter mais informações, consulte [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md).  
  
-   Pode ser mencionada como o destino de um parâmetro de cursor de saída em uma instrução EXECUTE se a variável não tiver um cursor atribuído no momento.  
  
-   Deve ser considerada como um ponteiro para o cursor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-declare"></a>A. Usando DECLARE  
 O exemplo a seguir usa uma variável local chamada `@find` para recuperar informações de contato para todos os sobrenomes que começam com `Man`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @find varchar(30);   
/* Also allowed:   
DECLARE @find varchar(30) = 'Man%';   
*/  
SET @find = 'Man%';   
SELECT p.LastName, p.FirstName, ph.PhoneNumber  
FROM Person.Person AS p   
JOIN Person.PersonPhone AS ph ON p.BusinessEntityID = ph.BusinessEntityID  
WHERE LastName LIKE @find;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName            FirstName               Phone
------------------- ----------------------- -------------------------
Manchepalli         Ajay                    1 (11) 500 555-0174
Manek               Parul                   1 (11) 500 555-0146
Manzanares          Tomas                   1 (11) 500 555-0178
  
(3 row(s) affected)
```  
  
### <a name="b-using-declare-with-two-variables"></a>b. Usando DECLARE com duas variáveis  
 O exemplo a seguir recupera os nomes de representantes de vendas do [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] localizados no território de vendas norte-americano que venderam pelo menos US$ 2.000.000 durante o ano.  
  
```  
USE AdventureWorks2012;  
GO  
SET NOCOUNT ON;  
GO  
DECLARE @Group nvarchar(50), @Sales money;  
SET @Group = N'North America';  
SET @Sales = 2000000;  
SET NOCOUNT OFF;  
SELECT FirstName, LastName, SalesYTD  
FROM Sales.vSalesPerson  
WHERE TerritoryGroup = @Group and SalesYTD >= @Sales;  
```  
  
### <a name="c-declaring-a-variable-of-type-table"></a>C. Declarando uma variável de tabela de tipos  
 O exemplo a seguir cria uma variável `table` que armazena os valores especificados na cláusula OUTPUT da instrução UPDATE. Seguem duas instruções `SELECT` que retornam os valores em `@MyTableVar` e os resultados da operação de atualização na tabela `Employee`. Observe que os resultados da coluna `INSERTED.ModifiedDate` são diferentes dos valores da coluna `ModifiedDate` na tabela `Employee`. Isso porque o gatilho `AFTER UPDATE`, que atualiza o valor de `ModifiedDate` com a data atual, está definido na tabela `Employee`. Porém, as colunas retornadas de `OUTPUT` refletem os dados antes de os gatilhos serem disparados. Para obter mais informações, confira [Cláusula OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
```  
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
  
### <a name="d-declaring-a-variable-of-user-defined-table-type"></a>D. Declarando uma variável de tipo de tabela definido pelo usuário  
 O exemplo a seguir cria um parâmetro com valor de tabela ou uma variável de tabela chamada `@LocationTVP`. Isso requer um tipo de tabela definido pelo usuário correspondente chamado `LocationTableType`. Para obter mais informações sobre como criar um tipo de tabela definido pelo usuário, consulte [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md). Para obter mais informações sobre parâmetros com valor de tabela, consulte [Usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
```  
DECLARE @LocationTVP   
AS LocationTableType;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-declare"></a>E. Usando DECLARE  
 O exemplo a seguir usa uma variável local chamada `@find` para recuperar informações de contato para todos os sobrenomes que começam com `Walt`.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @find varchar(30);  
/* Also allowed:   
DECLARE @find varchar(30) = 'Man%';  
*/  
SET @find = 'Walt%';  
  
SELECT LastName, FirstName, Phone  
FROM DimEmployee   
WHERE LastName LIKE @find;  
```  
  
### <a name="f-using-declare-with-two-variables"></a>F. Usando DECLARE com duas variáveis  
 O exemplo a seguir recupera e usa variáveis para especificar os nomes e sobrenomes de funcionários na tabela `DimEmployee`.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @lastName varchar(30), @firstName varchar(30);  
  
SET @lastName = 'Walt%';  
SET @firstName = 'Bryan';  
  
SELECT LastName, FirstName, Phone  
FROM DimEmployee   
WHERE LastName LIKE @lastName AND FirstName LIKE @firstName;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [Comparar XML tipado com XML não tipado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)  
  
  




