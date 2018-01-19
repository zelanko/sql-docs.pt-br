---
title: "A cláusula OUTPUT (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OUTPUT_TSQL
- OUTPUT
dev_langs: TSQL
helpviewer_keywords:
- displaying updated rows
- INSERT statement [SQL Server], OUTPUT clause
- outputs [SQL Server]
- OUTPUT clause
- row additions [SQL Server], OUTPUT clause
- viewing updated rows
- row deletions [SQL Server], OUTPUT clause
- viewing deleted rows
- DELETE statement [SQL Server], OUTPUT clause
- row updates [SQL Server]
- displaying inserted rows
- viewing inserted rows
- displaying deleted rows
- UPDATE statement [SQL Server], OUTPUT clause
ms.assetid: 41b9962c-0c71-4227-80a0-08fdc19f5fe4
caps.latest.revision: "94"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: a709097e12b435cbf32f88e13c067135aa3e77ad
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="output-clause-transact-sql"></a>cláusula OUTPUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações ou expressões baseadas em cada linha afetada por uma instrução INSERT, UPDATE, DELETE ou MERGE. Esses resultados podem ser retornados ao aplicativo de processamento para uso em mensagens de confirmação, arquivamentos e outros requisitos similares de aplicativo. Os resultados também podem ser inseridos em uma tabela ou variável de tabela. Além disso, você pode capturar os resultados de uma cláusula OUTPUT em uma instrução INSERT, UPDATE, DELETE, ou instrução MERGE e inserir esses resultados em uma tabela de destino ou exibição.  
  
> [!NOTE]  
>  Uma instrução UPDATE, INSERT ou DELETE que tem uma cláusula OUTPUT retornará linhas ao cliente mesmo que a instrução encontre erros e seja revertida. O resultado não deverá ser usado se ocorrer algum erro quando você executar a instrução.  
  
 **Usado em:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<OUTPUT_CLAUSE> ::=  
{  
    [ OUTPUT <dml_select_list> INTO { @table_variable | output_table } [ ( column_list ) ] ]  
    [ OUTPUT <dml_select_list> ]  
}  
<dml_select_list> ::=  
{ <column_name> | scalar_expression } [ [AS] column_alias_identifier ]  
    [ ,...n ]  
  
<column_name> ::=  
{ DELETED | INSERTED | from_table_name } . { * | column_name }  
    | $action  
```  
  
## <a name="arguments"></a>Argumentos  
 @*table_variable*  
 Especifica um **tabela** variável que as linhas retornadas são inseridas em vez de serem retornadas ao chamador. @*table_variable* deve ser declarado antes da instrução INSERT, UPDATE, DELETE ou MERGE.  
  
 Se *column_list* não for especificado, o **tabela** variável deve ter o mesmo número de colunas que o conjunto de resultados de saída. As colunas de identidade e as colunas computadas são exceções, que devem ser ignoradas. Se *column_list* for especificado, as colunas omitidas devem permitir valores nulos ou ter padrão valores atribuídos a eles.  
  
 Para obter mais informações sobre **tabela** variáveis, consulte [tabela &#40; Transact-SQL &#41; ](../../t-sql/data-types/table-transact-sql.md).  
  
 *output_table*  
 Especifica uma tabela na qual as linhas retornadas são inseridas, em vez de serem retornadas ao chamador. *output_table* pode ser uma tabela temporária.  
  
 Se *column_list* não for especificado, a tabela deve ter o mesmo número de colunas que o conjunto de resultados de saída. As colunas de identidade e as colunas computadas são exceções. Elas devem ser ignoradas. Se *column_list* for especificado, as colunas omitidas devem permitir valores nulos ou ter padrão valores atribuídos a eles.  
  
 *output_table* não pode:  
  
-   Ter gatilhos habilitados definidos.  
  
-   Participar de uma restrição FOREIGN KEY de nenhuma forma.  
  
-   Ter restrições CHECK ou regras habilitadas.  
  
*column_list*  
 É uma lista opcional de nomes de coluna na tabela de destino da cláusula INTO. Ele é semelhante à lista de colunas permitida no [inserir](../../t-sql/statements/insert-transact-sql.md) instrução.  
  
 *scalar_expression*  
 É qualquer combinação de símbolos e operadores que avalia um mesmo valor. Funções de agregação não são permitidas em *scalar_expression*.  
  
 Qualquer referência a colunas na tabela que está sendo modificada deve estar qualificada com o prefixo INSERTED ou DELETED.  
  
 *column_alias_identifier*  
 É um nome alternativo usado como referência ao nome de coluna.  
  
 DELETED  
 É um prefixo de coluna que especifica o valor excluído pela operação de atualização ou exclusão. Colunas prefixadas com DELETED refletem o valor antes de a instrução UPDATE, DELETE ou MERGE ser concluída.  
  
 DELETED não pode ser usado com a cláusula OUTPUT na instrução INSERT.  
  
 INSERTED  
 É um prefixo de coluna que especifica o valor adicionado pela operação de inserção ou atualização. Colunas prefixadas com INSERTED refletem o valor depois da conclusão da instrução UPDATE, INSERT ou MERGE, mas antes da execução dos gatilhos.  
  
 INSERTED não pode ser usado com a cláusula OUTPUT na instrução DELETE.  
  
 *from_table_name*  
 É um prefixo de coluna que especifica uma tabela incluída na cláusula FROM de uma instrução DELETE, UPDATE ou MERGE utilizada para especificar as linhas a serem atualizadas ou excluídas.  
  
 Se a tabela que está sendo modificada também estiver especificada na cláusula FROM, toda a referência a colunas nessa tabela também deverá estar qualificada com o prefixo INSERTED ou DELETED.  
  
 \*  
 Especifica que todas as colunas afetadas pela ação de exclusão, inserção ou atualização serão retornadas na ordem em que aparecem na tabela.  
  
 Por exemplo, `OUTPUT DELETED.*` na instrução DELETE a seguir retorna todas as colunas excluídas da tabela `ShoppingCartItem`:  
  
```  
DELETE Sales.ShoppingCartItem  
    OUTPUT DELETED.*;  
```  
  
 *column_name*  
 É uma referência de coluna explícita. Qualquer referência à tabela que está sendo modificada deve ser corretamente qualificada pelo INSERTED ou o prefixo excluídos conforme apropriado, por exemplo: INSERTED **. * * * column_name*.  
  
 $action  
 Está disponível apenas para a instrução MERGE. Especifica uma coluna do tipo **nvarchar (10)** na cláusula OUTPUT em uma instrução MERGE que retorna um dos três valores para cada linha: 'INSERT', 'UPDATE' ou 'DELETE', de acordo com a ação que foi executada na linha.  
  
## <a name="remarks"></a>Remarks  
 A saída \<dml_select_list > cláusula e a saída \<dml_select_list > INTO {**@ * table_variable* | *output_table* } podem ser definidas em uma única instrução de INSERT, UPDATE, DELETE ou MERGE.  
  
> [!NOTE]  
>  Salvo indicação em contrário, as referências à cláusula OUTPUT se referem tanto à cláusula OUTPUT, quanto à cláusula OUTPUT INTO.  
  
 A cláusula OUTPUT pode ser útil para recuperar o valor de identidade ou colunas computadas depois de uma operação INSERT ou UPDATE.  
  
 Quando uma coluna computada é incluída no \<dml_select_list >, a coluna correspondente na tabela de saída ou variável de tabela não é uma coluna computada. Os valores na nova coluna são aqueles que foram computados no momento em que a instrução foi executada.  
  
 Não há nenhuma garantia de que a ordem na qual as alterações são aplicadas à tabela e a ordem na qual as linhas são inseridas na tabela de saída ou na variável de tabela correspondam.  
  
 Se forem modificados parâmetros ou variáveis como parte de uma instrução UPDATE, a cláusula OUTPUT sempre retornará o valor do parâmetro ou a variável como era antes de a instrução ser executada, e não o valor modificado.  
  
 Você pode usar OUTPUT com uma instrução UPDATE ou DELETE posicionada em um cursor que use a sintaxe WHERE CURRENT OF.  
  
 Não há suporte para a cláusula OUTPUT nas seguintes instruções:  
  
-   Instruções DML que façam referência a exibições particionadas locais, exibições particionadas distribuídas ou tabelas remotas.  
  
-   Instruções INSERT contendo uma instrução EXECUTE.  
  
-   Não são permitidos predicados de texto completo na cláusula OUTPUT quando o nível de compatibilidade de banco de dados é definido como 100.  
  
-   A cláusula OUTPUT INTO não pode ser usada para inserção em uma exibição ou função de conjunto de linhas.  
  
-   Não é possível criar uma função definida pelo usuário caso ela contenha uma cláusula OUTPUT INTO que tenha uma tabela como seu destino.  
  
 Para impedir um comportamento não determinista, a cláusula OUTPUT não pode conter as referências a seguir:  
  
-   Subconsultas ou funções definidas pelo usuário que executam acesso a dados pelo usuário ou sistema ou que assumem que executam tal acesso. Supõe-se que as funções definidas pelo usuário executam acesso a dados quando não são associadas a esquema.  
  
-   Uma coluna de uma função com valor de tabela embutida ou exibição quando essa coluna é definida por um dos seguintes métodos:  
  
    -   Uma subconsulta.  
  
    -   Uma função definida pelo usuário que executa acesso a dados de usuário ou de sistema ou que supostamente executa tal acesso.  
  
    -   Uma coluna computada que contém uma função definida pelo usuário e que executa acesso a dados de usuário ou de sistema em sua definição.  
  
     Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detectar tal coluna na cláusula OUTPUT, ocorrerá o erro 4186.   
  
## <a name="inserting-data-returned-from-an-output-clause-into-a-table"></a>Inserindo dados retornados de uma cláusula OUTPUT em uma tabela  
 Ao capturar os resultados de uma cláusula OUTPUT em uma instrução INSERT, UPDATE, DELETE ou MERGE aninhada e inserir esses resultados em uma tabela ou exibição de destino, lembre-se do seguinte:  
  
-   Toda a operação é atômica. As instruções INSERT interna e DML aninhada que contêm a cláusula OUTPUT cláusula são executadas ou falham inteiramente.  
  
-   As seguintes restrições aplicam-se ao destino da instrução INSERT exterior:  
  
    -   O destino não pode ser uma tabela remota, exibição ou expressão de tabela comum.  
  
    -   O destino não pode ter uma restrição FOREIGN KEY nem ser referenciado por uma restrição FOREIGN KEY.  
  
    -   Não podem ser definidos gatilhos no destino.  
  
    -   O gatilho não pode participar de replicação de mesclagem ou de assinaturas atualizáveis para replicação transacional.  
  
-   As seguintes restrições aplicam-se à instrução DML aninhada:  
  
    -   O destino não pode ser uma tabela remota ou exibição particionada.  
  
    -   A própria origem não pode conter um \<dml_table_source > cláusula.  
  
-   Não há suporte para a cláusula OUTPUT INTO em instruções INSERT que contêm um \<dml_table_source > cláusula.  
  
-   @@ROWCOUNT retorna as linhas inseridas apenas pela instrução INSERT externa.  
  
-   @@IDENTITY, SCOPE_IDENTITY e IDENT_CURRENT retornam valores de identidade gerados apenas pela instrução DML aninhada e não os gerados pela instrução INSERT externa.  
  
-   As notificações de consulta tratam a instrução como uma única entidade, e o tipo de qualquer mensagem criada será o tipo DML aninhado, mesmo que alteração significativa seja proveniente da própria instrução INSERT.  
  
-   No \<dml_table_source > cláusula, SELECT e WHERE cláusulas não podem conter subconsultas, funções de agregação, funções de classificação, predicados de texto completo, funções definidas pelo usuário que executam acesso a dados ou a função TEXTPTR.  

## <a name="parallelism"></a>Paralelismo
 Uma cláusula OUTPUT que retorna resultados para o cliente sempre usará um plano serial.

No contexto de um banco de dados definido com nível de compatibilidade 130 ou superior, se uma instrução INSERT... Operação SELECT usa uma dica WITH (TABLOCK) para a instrução SELECT e também saída... INTO para inserir em uma tabela temporária ou de usuário e, em seguida, a tabela de destino para a instrução INSERT... Selecione estará qualificado para o paralelismo dependendo da subárvore de custo.  A tabela de destino referenciada na cláusula OUTPUT INTO não estará qualificada para o paralelismo. 
 
## <a name="triggers"></a>Gatilhos  
 Colunas retornadas de OUTPUT refletem os dados da forma em que se encontram após a conclusão da instrução UPDATE, INSERT ou MERGE, mas antes da execução dos gatilhos.  
  
 No caso dos gatilhos INSTEAD OF, os resultados retornados são gerados como se INSERT, UPDATE ou DELETE tivesse ocorrido de fato, mesmo que nenhuma modificação aconteça como resultado da operação do gatilho. Se uma instrução que inclui uma cláusula OUTPUT for usada dentro do corpo de um disparador, devem ser usados aliases de tabela para fazer referência às tabelas inseridas e excluídas pelo disparador, para evitar referências duplicadas a colunas com as tabelas INSERTED e DELETED associadas à OUTPUT.  
  
 Se a cláusula OUTPUT for especificada sem especificação da palavra-chave INTO, o destino da operação de DML não poderá ter um gatilho habilitado definido para a ação DML fornecida. Por exemplo, se a cláusula OUTPUT estiver definida em uma instrução UPDATE, a tabela de destino não poderá ter nenhum gatilho UPDATE habilitado.  
  
 Se a opção sp_configure disallow results from triggers estiver definida, uma cláusula OUTPUT sem cláusula INTO fará com que a instrução falhe quando ela for invocada a partir de um disparador.  
  
## <a name="data-types"></a>Tipos de dados  
 A cláusula OUTPUT oferece suporte a tipos de dados de objeto grande: **nvarchar (max)**, **varchar (max)**, **varbinary (max)**, **texto**, **ntext**, **imagem**, e **xml**. Quando você usa o. Cláusula de gravação na instrução UPDATE para modificar um **nvarchar (max)**, **varchar (max)**, ou **varbinary (max)** são de completo antes e depois imagens dos valores de coluna, retornado se eles são referenciados. A função TEXTPTR () não pode aparecer como parte de uma expressão em uma **texto**, **ntext**, ou **imagem** coluna na cláusula OUTPUT.  
  
## <a name="queues"></a>Filas  
 Você pode usar OUTPUT em aplicativos que usam tabelas como filas ou para manter conjuntos de resultados intermediários. Ou seja, o aplicativo está somando ou removendo linhas constantemente da tabela. O exemplo a seguir usa a cláusula OUTPUT em uma instrução DELETE para retornar a linha excluída para o aplicativo de chamada.  
  
```  
USE AdventureWorks2012;  
GO  
DELETE TOP(1) dbo.DatabaseLog WITH (READPAST)  
OUTPUT deleted.*  
WHERE DatabaseLogID = 7;  
GO  
  
```  
  
 Este exemplo remove uma linha de uma tabela usada como fila e retorna os valores excluídos para o aplicativo de processamento em uma única ação. Outras semânticas também podem ser implementadas, como usar uma tabela para implementar uma pilha. Porém, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não garante a ordem em que as linhas são processadas e retornadas por instruções DML que usam a cláusula OUTPUT. Cabe ao aplicativo incluir uma cláusula WHERE apropriada que possa garantir a semântica desejada ou entender que, quando várias linhas puderem se qualificar para a operação DML, não haverá nenhuma garantia de ordem. O exemplo a seguir usa uma subconsulta e presume que exclusividade seja uma característica da coluna `DatabaseLogID` para implementar a semântica de ordenação desejada.  
  
```  
USE tempdb;  
GO  
CREATE TABLE dbo.table1  
(  
    id INT,  
    employee VARCHAR(32)  
);  
GO  
  
INSERT INTO dbo.table1 VALUES   
      (1, 'Fred')  
     ,(2, 'Tom')  
     ,(3, 'Sally')  
     ,(4, 'Alice');  
GO  
  
DECLARE @MyTableVar TABLE  
(  
    id INT,  
    employee VARCHAR(32)  
);  
  
PRINT 'table1, before delete'   
SELECT * FROM dbo.table1;  
  
DELETE FROM dbo.table1  
OUTPUT DELETED.* INTO @MyTableVar  
WHERE id = 4 OR id = 2;  
  
PRINT 'table1, after delete'  
SELECT * FROM dbo.table1;  
  
PRINT '@MyTableVar, after delete'  
SELECT * FROM @MyTableVar;  
  
DROP TABLE dbo.table1;  
  
--Results  
--table1, before delete  
--id          employee  
------------- ------------------------------  
--1           Fred  
--2           Tom  
--3           Sally  
--4           Alice  
--  
--table1, after delete  
--id          employee  
------------- ------------------------------  
--1           Fred  
--3           Sally  
--@MyTableVar, after delete  
--id          employee  
------------- ------------------------------  
--2           Tom  
--4           Alice  
  
```  
  
> [!NOTE]  
>  Use a dica de tabela READPAST nas instruções UPDATE e DELETE, se o cenário permitir que vários aplicativos executem uma leitura destrutiva de uma tabela. Isso impedirá que venham a acontecer problemas de bloqueios, caso outro aplicativo já esteja lendo o primeiro registro de qualificação na tabela.  
  
## <a name="permissions"></a>Permissões  
 São necessárias permissões SELECT nas colunas recuperadas por meio de \<dml_select_list > ou usadas em \<scalar_expression >.  
  
 São necessárias permissões de INSERT em tabelas especificadas em \<output_table >.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-output-into-with-a-simple-insert-statement"></a>A. Usando OUTPUT INTO com uma instrução INSERT simples  
 O exemplo a seguir insere uma linha para o `ScrapReason` tabela e usa o `OUTPUT` cláusula para retornar os resultados da instrução para o `@MyTableVar``table` variável. Como a coluna `ScrapReasonID` está definida com uma propriedade IDENTITY, não é especificado um valor na instrução `INSERT` dessa coluna. Porém, note que o valor gerado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] para a coluna é retornado na cláusula `OUTPUT` na coluna `inserted.ScrapReasonID`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table( NewScrapReasonID smallint,  
                           Name varchar(50),  
                           ModifiedDate datetime);  
INSERT Production.ScrapReason  
    OUTPUT INSERTED.ScrapReasonID, INSERTED.Name, INSERTED.ModifiedDate  
        INTO @MyTableVar  
VALUES (N'Operator error', GETDATE());  
  
--Display the result set of the table variable.  
SELECT NewScrapReasonID, Name, ModifiedDate FROM @MyTableVar;  
--Display the result set of the table.  
SELECT ScrapReasonID, Name, ModifiedDate   
FROM Production.ScrapReason;  
GO  
  
```  
  
### <a name="b-using-output-with-a-delete-statement"></a>B. Usando OUTPUT com uma instrução DELETE  
 O exemplo a seguir exclui todas as linhas da tabela `ShoppingCartItem`. A cláusula `OUTPUT deleted.*` especifica que os resultados da instrução `DELETE`, que são todas as colunas nas linhas excluídas, sejam retornados para o aplicativo de chamada. A instrução `SELECT` que segue verifica os resultados da operação de exclusão na tabela `ShoppingCartItem`.  
  
```  
USE AdventureWorks2012;  
GO  
DELETE Sales.ShoppingCartItem  
OUTPUT DELETED.*   
WHERE ShoppingCartID = 20621;  
  
--Verify the rows in the table matching the WHERE clause have been deleted.  
SELECT COUNT(*) AS [Rows in Table] FROM Sales.ShoppingCartItem WHERE ShoppingCartID = 20621;  
GO  
  
```  
  
### <a name="c-using-output-into-with-an-update-statement"></a>C. Usando OUTPUT INTO com uma instrução UPDATE  
 O exemplo a seguir atualiza a coluna `VacationHours` na tabela `Employee` em 25% nas primeiras 10 linhas. O `OUTPUT` cláusula retorna o `VacationHours` valor existe antes de aplicar o `UPDATE` instrução na coluna `deleted.VacationHours`e o valor atualizado na coluna `inserted.VacationHours` para o `@MyTableVar``table` variável.  
  
 Seguem duas instruções `SELECT` que retornam os valores em `@MyTableVar` e os resultados da operação de atualização na tabela `Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()   
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
  
```  
  
### <a name="d-using-output-into-to-return-an-expression"></a>D. Usando OUTPUT INTO para retornar uma expressão  
 O exemplo a seguir se baseia no exemplo C, definindo uma expressão na cláusula `OUTPUT` como diferença entre o valor `VacationHours` atualizado e o valor `VacationHours` antes de a atualização ser aplicada. O valor dessa expressão é retornado para o `@MyTableVar``table` variável na coluna `VacationHoursDifference`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    VacationHoursDifference int,  
    ModifiedDate datetime);  
  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()  
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.VacationHours - deleted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours,   
    VacationHoursDifference, ModifiedDate  
FROM @MyTableVar;  
GO  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
  
```  
  
### <a name="e-using-output-into-with-fromtablename-in-an-update-statement"></a>E. Usando OUTPUT INTO com from_table_name em uma instrução UPDATE  
 A exemplo a seguir atualiza o `ScrapReasonID` coluna o `WorkOrder` tabela para todas as ordens de trabalho com um especificado `ProductID` e `ScrapReasonID`. A cláusula `OUTPUT INTO` retorna valores da tabela que está sendo atualizada (`WorkOrder`) e também da tabela `Product`. A tabela `Product` é usada na cláusula `FROM` para especificar as linhas a serem atualizadas. Como a tabela `WorkOrder` tem um gatilho `AFTER UPDATE` definido, é necessária a palavra-chave `INTO`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTestVar table (  
    OldScrapReasonID int NOT NULL,   
    NewScrapReasonID int NOT NULL,   
    WorkOrderID int NOT NULL,  
    ProductID int NOT NULL,  
    ProductName nvarchar(50)NOT NULL);  
  
UPDATE Production.WorkOrder  
SET ScrapReasonID = 4  
OUTPUT deleted.ScrapReasonID,  
       inserted.ScrapReasonID,   
       inserted.WorkOrderID,  
       inserted.ProductID,  
       p.Name  
    INTO @MyTestVar  
FROM Production.WorkOrder AS wo  
    INNER JOIN Production.Product AS p   
    ON wo.ProductID = p.ProductID   
    AND wo.ScrapReasonID= 16  
    AND p.ProductID = 733;  
  
SELECT OldScrapReasonID, NewScrapReasonID, WorkOrderID,   
    ProductID, ProductName   
FROM @MyTestVar;  
GO  
  
```  
  
### <a name="f-using-output-into-with-fromtablename-in-a-delete-statement"></a>F. Usando OUTPUT INTO com from_table_name em uma instrução DELETE  
 O exemplo a seguir exclui linhas da tabela `ProductProductPhoto` com base em critérios de pesquisa definidos na cláusula `FROM` da instrução `DELETE`. A cláusula `OUTPUT` retorna colunas da tabela que está sendo excluída (`deleted.ProductID`, `deleted.ProductPhotoID`) e colunas da tabela `Product`. Essa tabela é usada na cláusula `FROM` para especificar as linhas a serem excluídas.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    ProductID int NOT NULL,   
    ProductName nvarchar(50)NOT NULL,  
    ProductModelID int NOT NULL,   
    PhotoID int NOT NULL);  
  
DELETE Production.ProductProductPhoto  
OUTPUT DELETED.ProductID,  
       p.Name,  
       p.ProductModelID,  
       DELETED.ProductPhotoID  
    INTO @MyTableVar  
FROM Production.ProductProductPhoto AS ph  
JOIN Production.Product as p   
    ON ph.ProductID = p.ProductID   
    WHERE p.ProductModelID BETWEEN 120 and 130;  
  
--Display the results of the table variable.  
SELECT ProductID, ProductName, ProductModelID, PhotoID   
FROM @MyTableVar  
ORDER BY ProductModelID;  
GO  
  
```  
  
### <a name="g-using-output-into-with-a-large-object-data-type"></a>G. Usando OUTPUT INTO com um tipo de dados de objeto grande  
 O exemplo a seguir atualiza um valor parcial em `DocumentSummary` e uma coluna `nvarchar(max)` na tabela `Production.Document` usando a cláusula `.WRITE`. A palavra `components` é substituída pela palavra `features` especificando a palavra de substituição, o local de início (deslocamento) da palavra a ser substituído em dados existentes e o número de caracteres a serem substituídos (comprimento). O exemplo usa o `OUTPUT` cláusula para retornar o antes e depois de imagens do `DocumentSummary` coluna para o `@MyTableVar``table` variável. Observe que são retornadas as imagens completas de antes e depois da coluna `DocumentSummary`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    SummaryBefore nvarchar(max),  
    SummaryAfter nvarchar(max));  
  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
OUTPUT deleted.DocumentSummary,   
       inserted.DocumentSummary   
    INTO @MyTableVar  
WHERE Title = N'Front Reflector Bracket Installation';  
  
SELECT SummaryBefore, SummaryAfter   
FROM @MyTableVar;  
GO  
  
```  
  
### <a name="h-using-output-in-an-instead-of-trigger"></a>H. Usando OUTPUT em um gatilho INSTEAD OF  
 O exemplo a seguir usa a cláusula `OUTPUT` em um gatilho para retornar os resultados da operação do gatilho. Primeiro, uma exibição é criada na tabela `ScrapReason` e, em seguida, um gatilho `INSTEAD OF INSERT` é definido na exibição, permitindo que apenas a coluna `Name` da tabela base seja modificada pelo usuário. Como a coluna `ScrapReasonID` é uma coluna `IDENTITY` na tabela base, o gatilho ignora o valor fornecido pelo usuário. Isso permite ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] gerar o valor correto automaticamente. O valor fornecido pelo usuário para `ModifiedDate` também é ignorado, sendo definido como a data atual. A cláusula `OUTPUT` retorna os valores inseridos de fato na tabela `ScrapReason`.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('dbo.vw_ScrapReason','V') IS NOT NULL  
    DROP VIEW dbo.vw_ScrapReason;  
GO  
CREATE VIEW dbo.vw_ScrapReason  
AS (SELECT ScrapReasonID, Name, ModifiedDate  
    FROM Production.ScrapReason);  
GO  
CREATE TRIGGER dbo.io_ScrapReason   
    ON dbo.vw_ScrapReason  
INSTEAD OF INSERT  
AS  
BEGIN  
--ScrapReasonID is not specified in the list of columns to be inserted   
--because it is an IDENTITY column.  
    INSERT INTO Production.ScrapReason (Name, ModifiedDate)  
        OUTPUT INSERTED.ScrapReasonID, INSERTED.Name,   
               INSERTED.ModifiedDate  
    SELECT Name, getdate()  
    FROM inserted;  
END  
GO  
INSERT vw_ScrapReason (ScrapReasonID, Name, ModifiedDate)  
VALUES (99, N'My scrap reason','20030404');  
GO  
  
```  
  
 Eis o conjunto de resultados gerado no dia 12 de abril de 2004 ('`2004-04-12'`). Observe que as colunas `ScrapReasonIDActual` e `ModifiedDate` refletem os valores gerados pela operação do gatilho, no lugar dos valores fornecidos na instrução `INSERT`.  
  
 ```
 ScrapReasonID  Name             ModifiedDate  
 -------------  ---------------- -----------------------  
 17             My scrap reason  2004-04-12 16:23:33.050
 ```  
  
### <a name="i-using-output-into-with-identity-and-computed-columns"></a>I. Usando OUTPUT INTO com colunas de identidade e colunas computadas  
 O exemplo a seguir cria a tabela `EmployeeSales` e, em seguida, insere várias linhas nela por meio de uma instrução `INSERT` com uma instrução `SELECT`, para recuperar dados das tabelas de origem. A tabela `EmployeeSales` contém uma coluna de identidade (`EmployeeID`) e uma coluna computada (`ProjectedSales`).  
  
```  
USE AdventureWorks2012 ;  
GO  
IF OBJECT_ID ('dbo.EmployeeSales', 'U') IS NOT NULL  
    DROP TABLE dbo.EmployeeSales;  
GO  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   int IDENTITY (1,5)NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales AS CurrentSales * 1.10   
);  
GO  
DECLARE @MyTableVar table(  
  EmployeeID   int NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales money NOT NULL  
  );  
  
INSERT INTO dbo.EmployeeSales (LastName, FirstName, CurrentSales)  
  OUTPUT INSERTED.LastName,   
         INSERTED.FirstName,   
         INSERTED.CurrentSales  
  INTO @MyTableVar  
    SELECT c.LastName, c.FirstName, sp.SalesYTD  
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY c.LastName, c.FirstName;  
  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM @MyTableVar;  
GO  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM dbo.EmployeeSales;  
GO  
  
```  
  
### <a name="j-using-output-and-output-into-in-a-single-statement"></a>J. Usando OUTPUT e OUTPUT INTO em uma única instrução  
 O exemplo a seguir exclui linhas da tabela `ProductProductPhoto` com base em critérios de pesquisa definidos na cláusula `FROM` da instrução `DELETE`. O `OUTPUT INTO` cláusula retorna colunas da tabela que está sendo excluída (`deleted.ProductID`, `deleted.ProductPhotoID`) e colunas do `Product` de tabela para o `@MyTableVar``table` variável. A tabela `Product` é usada na cláusula `FROM` para especificar as linhas a serem excluídas. A cláusula `OUTPUT` retorna as colunas `deleted.ProductID` e `deleted.ProductPhotoID` e a data e a hora em que a linha foi excluída da tabela `ProductProductPhoto` ao aplicativo de chamada.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    ProductID int NOT NULL,   
    ProductName nvarchar(50)NOT NULL,  
    ProductModelID int NOT NULL,   
    PhotoID int NOT NULL);  
  
DELETE Production.ProductProductPhoto  
OUTPUT DELETED.ProductID,  
       p.Name,  
       p.ProductModelID,  
       DELETED.ProductPhotoID  
    INTO @MyTableVar  
OUTPUT DELETED.ProductID, DELETED.ProductPhotoID, GETDATE() AS DeletedDate   
FROM Production.ProductProductPhoto AS ph  
JOIN Production.Product as p   
    ON ph.ProductID = p.ProductID   
WHERE p.ProductID BETWEEN 800 and 810;  
  
--Display the results of the table variable.  
SELECT ProductID, ProductName, PhotoID, ProductModelID   
FROM @MyTableVar;  
GO  
  
```  
  
### <a name="k-inserting-data-returned-from-an-output-clause"></a>K. Inserindo dados retornados de uma cláusula OUTPUT  
 O exemplo a seguir captura dados retornados da cláusula `OUTPUT` de uma instrução `MERGE` e insere esses dados em outra tabela. A instrução `MERGE` atualiza a coluna `Quantity` da tabela `ProductInventory` diariamente, com base nos pedidos processados na tabela `SalesOrderDetail`. Ela também exclui linhas de produtos cujos inventários caem para `0` ou menos. O exemplo captura as linhas excluídas e as insere em outra tabela, `ZeroInventory`, que rastreia produtos sem-estoque.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Production.ZeroInventory', N'U') IS NOT NULL  
    DROP TABLE Production.ZeroInventory;  
GO  
--Create ZeroInventory table.  
CREATE TABLE Production.ZeroInventory (DeletedProductID int, RemovedOnDate DateTime);  
GO  
  
INSERT INTO Production.ZeroInventory (DeletedProductID, RemovedOnDate)  
SELECT ProductID, GETDATE()  
FROM  
(   MERGE Production.ProductInventory AS pi  
    USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
           JOIN Sales.SalesOrderHeader AS soh  
           ON sod.SalesOrderID = soh.SalesOrderID  
           AND soh.OrderDate = '20070401'  
           GROUP BY ProductID) AS src (ProductID, OrderQty)  
    ON (pi.ProductID = src.ProductID)  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0  
        THEN DELETE  
    WHEN MATCHED  
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    OUTPUT $action, deleted.ProductID) AS Changes (Action, ProductID)  
WHERE Action = 'DELETE';  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were inserted';  
GO  
SELECT DeletedProductID, RemovedOnDate FROM Production.ZeroInventory;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERIR &#40;O Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [table &#40;Transact-SQL&#41;](../../t-sql/data-types/table-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
