---
title: DELETE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DELETE
- DELETE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row removal [SQL Server]
- DELETE statement [SQL Server], about DELETE statement
- views [SQL Server], deleting rows
- removing rows
- tables [SQL Server], deleting rows
- DELETE statement [SQL Server]
- deleting rows
- row removal [SQL Server], DELETE statement
- deleting data
ms.assetid: ed6b2105-0f35-408f-ba51-e36ade7ad5b2
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bcf25195821c42d5120fc5d248b364ce23e24ed0
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51700314"
---
# <a name="delete-transact-sql"></a>DELETE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Remove uma ou mais linhas de uma tabela ou exibição no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ WITH <common_table_expression> [ ,...n ] ]  
DELETE   
    [ TOP ( expression ) [ PERCENT ] ]   
    [ FROM ]   
    { { table_alias  
      | <object>   
      | rowset_function_limited   
      [ WITH ( table_hint_limited [ ...n ] ) ] }   
      | @table_variable  
    }  
    [ <OUTPUT Clause> ]  
    [ FROM table_source [ ,...n ] ]   
    [ WHERE { <search_condition>   
            | { [ CURRENT OF   
                   { { [ GLOBAL ] cursor_name }   
                       | cursor_variable_name   
                   }   
                ]  
              }  
            }   
    ]   
    [ OPTION ( <Query Hint> [ ,...n ] ) ]   
[; ]  
  
<object> ::=  
{   
    [ server_name.database_name.schema_name.   
      | database_name. [ schema_name ] .   
      | schema_name.  
    ]  
    table_or_view_name   
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DELETE FROM [database_name . [ schema ] . | schema. ] table_name    
    [ WHERE <search_condition> ]   
    [ OPTION ( <query_options> [ ,...n ]  ) ]  
[; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 WITH \<common_table_expression>  
 Especifica o conjunto de resultados nomeados temporário, também conhecido como expressão de tabela comum, definido dentro do escopo da instrução DELETE. O conjunto de resultados é derivado de uma instrução SELECT.  
  
 Também podem ser usadas expressões de tabela comuns com as instruções SELECT, INSERT, UPDATE e CREATE VIEW. Para obter mais informações, confira [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 TOP **(**_expression_**)** [ PERCENT ]  
 Especifica o número ou a porcentagem de linhas aleatórias que serão excluídas. *expression* pode ser um número ou uma porcentagem das linhas. As linhas referenciadas na expressão TOP usada com INSERT, UPDATE ou DELETE não são organizadas em qualquer ordem. Para obter mais informações, confira [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
 FROM  
 Uma palavra-chave opcional que pode ser usada entre a palavra-chave DELETE e *table_or_view_name* ou *rowset_function_limited* de destino.  
  
 *table_alias*  
 O alias especificado na cláusula FROM *table_source* que representa a tabela ou exibição na qual as linhas devem ser excluídas.  
  
 *server_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 O nome do servidor (que usa um nome de servidor vinculado ou a função [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) como nome do servidor) no qual a tabela ou exibição está localizada. Se *server_name* for especificado, *database_name* e *schema_name* serão necessários.  
  
 *database_name*  
 O nome do banco de dados.  
  
 *schema_name*  
 O nome do esquema ao qual a tabela ou exibição pertence.  
  
 *table_or_view_name*  
 O nome da tabela ou exibição da qual as linhas serão removidas.  
  
 Uma variável de tabela, dentro de seu escopo, também pode ser usada como origem da tabela em uma instrução DELETE.  
  
 A exibição referenciada por *table_or_view_name* deve ser atualizável e referenciar exatamente uma tabela base na cláusula FROM da definição de exibição. Para obter mais informações sobre exibições atualizáveis, consulte [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 *rowset_function_limited*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 A função [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) ou [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md), sujeita às funcionalidades do provedor.  
  
 WITH **(** \<table_hint_limited> [... *n*] **)**  
 Especifica uma ou mais dicas de tabela permitidas para uma tabela de destino. A palavra-chave WITH e parênteses são necessários. NOLOCK e READUNCOMMITTED não são permitidos. Para obter mais informações sobre dicas de tabela, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 \<OUTPUT_Clause>  
 Retorna linhas excluídas, ou expressões baseadas nelas, como parte da operação DELETE. A cláusula OUTPUT não tem suporte em nenhuma instrução DML destinada a exibições ou tabelas remotas. Para obter mais informações, confira [Cláusula OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
 FROM *table_source*  
 Especifica uma cláusula FROM adicional. Essa extensão [!INCLUDE[tsql](../../includes/tsql-md.md)] para DELETE permite especificar dados de \<table_source> e excluir as linhas correspondentes da tabela na primeira cláusula FROM.  
  
 Essa extensão, especificando uma união, pode ser usada em vez de uma subconsulta na cláusula WHERE para identificar linhas a serem removidas.  
  
 Para obter mais informações, consulte [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
 WHERE  
 Especifica as condições usadas para limitar o número de linhas que são excluídas. Se uma cláusula WHERE não for fornecida, DELETE removerá todas as linhas da tabela.  
  
 Há duas formas de excluir operações com base no que é especificado na cláusula WHERE:  
  
-   Exclusões pesquisadas especificam um critério de pesquisa para qualificar as linhas a serem excluídas. Por exemplo, WHERE *column_name* = *value*.  
  
-   Exclusões posicionadas usam a cláusula CURRENT OF para especificar um cursor. A operação de exclusão ocorre na posição atual do cursor. Isso pode ser mais preciso do que uma instrução DELETE pesquisada que usa uma cláusula WHERE *search_condition* para qualificar as linhas a serem excluídas. Uma instrução DELETE pesquisada exclui várias linhas se o critério de pesquisa não identificar exclusivamente uma única linha.  
  
\<search_condition>  
 Especifica os critérios de restrição para as linhas a serem excluídas. Não há nenhum limite para o número de predicados que podem ser incluídos em um critério de pesquisa. Para obter mais informações, consulte [Condição de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 CURRENT OF  
 Especifica que DELETE é executado na posição atual do cursor especificado.  
  
 GLOBAL  
 Especifica que *cursor_name* se refere a um cursor global.  
  
 *cursor_name*  
 É o nome do cursor aberto do qual a busca é feita. Se um cursor global e um cursor local com o nome *cursor_name* existirem, esse argumento fará referência ao cursor global se GLOBAL estiver especificado; caso contrário, fará referência ao cursor local. O cursor deve permitir atualizações.  
  
 *cursor_variable_name*  
 O nome de uma variável de cursor. A variável de cursor deve fazer referência a um cursor que permite atualizações.  
  
 OPTION **(** \<query_hint> [ **,**... *n*] **)**  
 Palavras-chave que indicam as dicas de otimização que são usadas para personalizar a forma como o [!INCLUDE[ssDE](../../includes/ssde-md.md)] processa a instrução. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Para excluir todas as linhas em uma tabela, use TRUNCATE TABLE. TRUNCATE TABLE é mais rápido que DELETE e usa menos recursos do sistema e do log de transações. TRUNCATE TABLE tem restrições; por exemplo, a tabela não pode participar da replicação. Para obter mais informações, veja [TRUNCATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/truncate-table-transact-sql.md)  
  
 Use a função @@ROWCOUNT para retornar o número de linhas excluídas para o aplicativo cliente. Para obter mais informações, consulte [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md).  
  
## <a name="error-handling"></a>Tratamento de erros  
 Você pode implementar o tratamento de erros para a instrução DELETE especificando a instrução em uma construção TRY…CATCH.  
  
 A instrução DELETE pode falhar se violar um gatilho ou tentar remover uma linha referenciada por dados em outra tabela com uma restrição FOREIGN KEY. Se DELETE remover várias linhas e qualquer uma das linhas removidas violar um gatilho ou uma restrição, a instrução será cancelada, um erro será retornado e nenhuma linha será removida.  
  
 Quando uma instrução DELETE encontra um erro aritmético (estouro, divisão por zero ou um erro de domínio) que ocorre durante a avaliação de expressão, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] trata esses erros como se SET ARITHABORT estivesse definido como ON. O restante do lote é cancelado e uma mensagem de erro é retornada.  
  
## <a name="interoperability"></a>Interoperabilidade  
 DELETE poderá ser usado no corpo de uma função definida pelo usuário se o objeto modificado for uma variável de tabela.  
  
 Ao excluir uma linha que contém uma coluna FILESTREAM, você também excluirá os arquivos subjacentes do sistema de arquivos. Os arquivos subjacentes são removidos pelo coletor de lixo do FILESTREAM. Para obter mais informações, veja [Acessar Dados FILESTREAM com Transact-SQL](../../relational-databases/blob/access-filestream-data-with-transact-sql.md).  
  
 A cláusula FROM não pode ser especificada em uma instrução DELETE que faça referência, direta ou indiretamente, a uma exibição com um gatilho INSTEAD OF definido. Para obter mais informações sobre gatilhos INSTEAD OF, confira [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Quando TOP é usado com DELETE, as linhas referenciadas não são organizadas em ordem alguma e a cláusula ORDER BY não pode ser especificada diretamente nessa instrução. Se você precisar usar TOP para excluir linhas em uma ordem cronológica significativa, será preciso usar TOP junto com uma cláusula ORDER BY em uma instrução de subseleção. Consulte a seção Exemplos a seguir neste tópico.  
  
 TOP não pode ser usado em uma DELETE instrução para exibições particionadas.  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 Por padrão, uma instrução DELETE sempre adquire um bloqueio exclusivo (X) na tabela que modifica e mantém esse bloqueio até que a transação seja concluída. Com um bloqueio exclusivo (X), nenhuma outra transação pode modificar os dados; operações de leitura podem ser realizadas apenas com o uso da dica NOLOCK ou nível de isolamento de leitura não confirmada. Você pode especificar dicas de tabela para substituir esse comportamento padrão durante a instrução DELETE especificando outro método de bloqueio; entretanto, é recomendável que as dicas só sejam usadas como último recurso por desenvolvedores experientes e administradores de bancos de dados. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Quando linhas são excluídas de um heap, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode usar bloqueio de linha ou página para a operação. Como resultado, as páginas que ficaram vazias pela operação de exclusão permanecem alocadas no heap. Quando páginas vazias não são desalocadas, o espaço associado não pode ser usado novamente por outros objetos do banco de dados.  
  
 Para excluir linhas em um heap e desalocar páginas, use um dos seguintes métodos.  
  
-   Especifique a dica TABLOCK na instrução DELETE. Usar a dica TABLOCK faz com que a operação de exclusão use um bloqueio exclusivo na tabela em vez de um bloqueio de linha ou página. Isso permite que as páginas sejam desalocadas. Para obter mais informações sobre a dica TABLOCK, veja [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
-   Use TRUNCATE TABLE se todas as linhas forem excluídas da tabela.  
  
-   Crie um índice clusterizado no heap antes de excluir as linhas. Você pode cancelar o índice clusterizado depois que as linhas forem excluídas. Esse método consome mais tempo do que os métodos anteriores e usa mais recursos temporários.  
  
> [!NOTE]  
>  Páginas vazias podem ser removidas de um heap a qualquer momento usando a instrução `ALTER TABLE <table_name> REBUILD`.  
  
## <a name="logging-behavior"></a>Comportamento de log  
 A DELETE instrução sempre é registrada em log completamente.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 São necessárias permissões DELETE na tabela de destino. Também serão necessárias permissões SELECT se a instrução tiver uma cláusula WHERE.  
  
 As permissões DELETE assumem como padrão os membros da função de servidor fixa **sysadmin**, as funções de banco de dados fixa **db_owner** e **db_datawriter** e o proprietário da tabela. Os membros das funções **sysadmin**, **db_owner** e **db_securityadmin** e o proprietário da tabela podem transferir permissões para outros usuários.  
  
## <a name="examples"></a>Exemplos  
  
|Categoria|Elementos de sintaxe em destaque|  
|--------------|------------------------------|  
|[Sintaxe básica](#BasicSyntax)|Delete (excluir)|  
|[Limitando as linhas excluídas](#LimitRows)|WHERE • FROM • cursor •|  
|[Excluindo linhas de uma tabela remota](#RemoteTables)|Servidor vinculado • Função de conjunto de linhas OPENQUERY • Função de conjunto de linhas OPENDATASOURCE|  
|[Capturando os resultados da instrução DELETE](#CaptureResults)|cláusula OUTPUT|  
  
###  <a name="BasicSyntax"></a> Sintaxe básica  
 Os exemplos nesta seção demonstram a funcionalidade básica da instrução DELETE usando a sintaxe mínima necessária.  
  
#### <a name="a-using-delete-with-no-where-clause"></a>A. Usando DELETE sem a cláusula WHERE  
 O exemplo a seguir exclui todas as linhas de uma tabela `SalesPersonQuotaHistory` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] porque uma cláusula WHERE não é usada para limitar o número de linhas excluídas.  
  
```sql
DELETE FROM Sales.SalesPersonQuotaHistory;  
GO  
```  
  
###  <a name="LimitRows"></a> Limitando as linhas excluídas  
 Exemplos nesta seção demonstram como limitar o número de linhas que serão excluídas.  
  
#### <a name="b-using-the-where-clause-to-delete-a-set-of-rows"></a>B. Usando a cláusula WHERE para excluir um conjunto de linhas  
 O exemplo a seguir exclui todas as linhas de uma tabela `ProductCostHistory` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] na qual o valor da coluna `StandardCost` é maior que `1000.00`.  
  
```sql
DELETE FROM Production.ProductCostHistory  
WHERE StandardCost > 1000.00;  
GO  
```  
  
 O exemplo a seguir mostra uma cláusula WHERE mais complexa. A cláusula WHERE define duas condições que devem ser atendidas para determinar as linhas a serem excluídas. O valor na coluna `StandardCost` deve ser entre `12.00` e `14.00` , e o valor na coluna `SellEndDate` deve ser nulo. O exemplo também imprime o valor da função **@@ROWCOUNT** para retornar o número de linhas excluídas.  
  
```sql
DELETE Production.ProductCostHistory  
WHERE StandardCost BETWEEN 12.00 AND 14.00  
      AND EndDate IS NULL;  
PRINT 'Number of rows deleted is ' + CAST(@@ROWCOUNT as char(3));  
```  
  
#### <a name="c-using-a-cursor-to-determine-the-row-to-delete"></a>C. Usando um cursor para determinar a linha a ser excluída  
 O exemplo a seguir exclui uma única linha da tabela `EmployeePayHistory` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] que usa um cursor nomeado `my_cursor`. O operação de exclusão afeta somente a única linha buscada atualmente pelo cursor.  
  
```sql
DECLARE complex_cursor CURSOR FOR  
    SELECT a.BusinessEntityID  
    FROM HumanResources.EmployeePayHistory AS a  
    WHERE RateChangeDate <>   
         (SELECT MAX(RateChangeDate)  
          FROM HumanResources.EmployeePayHistory AS b  
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;  
OPEN complex_cursor;  
FETCH FROM complex_cursor;  
DELETE FROM HumanResources.EmployeePayHistory  
WHERE CURRENT OF complex_cursor;  
CLOSE complex_cursor;  
DEALLOCATE complex_cursor;  
GO  
```  
  
#### <a name="d-using-joins-and-subqueries-to-data-in-one-table-to-delete-rows-in-another-table"></a>D. Usando junções e subconsultas para dados em uma tabela para excluir linhas em outra tabela  
 Os exemplos a seguir mostram dois modos de excluir linhas em uma tabela com base em dados de outra tabela. Nos dois exemplos, as linhas da tabela `SalesPersonQuotaHistory` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] são excluídas com base nas vendas acumuladas no ano armazenadas na tabela `SalesPerson`. A primeira instrução `DELETE` mostra a solução de subconsulta compatível com ISO e a segunda instrução `DELETE` mostra a extensão FROM [!INCLUDE[tsql](../../includes/tsql-md.md)] para unir as duas tabelas.  
  
```sql
-- SQL-2003 Standard subquery  
  
DELETE FROM Sales.SalesPersonQuotaHistory   
WHERE BusinessEntityID IN   
    (SELECT BusinessEntityID   
     FROM Sales.SalesPerson   
     WHERE SalesYTD > 2500000.00);  
GO  
```  
  
```sql
-- Transact-SQL extension  
  
DELETE FROM Sales.SalesPersonQuotaHistory   
FROM Sales.SalesPersonQuotaHistory AS spqh  
INNER JOIN Sales.SalesPerson AS sp  
ON spqh.BusinessEntityID = sp.BusinessEntityID  
WHERE sp.SalesYTD > 2500000.00;  
GO  
```  
  
```sql
-- No need to mention target table more than once.  
  
DELETE spqh  
  FROM  
        Sales.SalesPersonQuotaHistory AS spqh  
    INNER JOIN Sales.SalesPerson AS sp  
        ON spqh.BusinessEntityID = sp.BusinessEntityID  
  WHERE  sp.SalesYTD > 2500000.00;  
```  
  
#### <a name="e-using-top-to-limit-the-number-of-rows-deleted"></a>E. Usando TOP para limitar o número de linhas excluídas  
 Quando uma cláusula TOP (*n*) é usada com DELETE, a operação de exclusão é executada em uma seleção aleatória de um número *n* de linhas. O exemplo a seguir exclui `20` linhas aleatórias da tabela `PurchaseOrderDetail` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] que têm datas de vencimento anteriores a 1º de julho de 2006.  
  
```sql
DELETE TOP (20)   
FROM Purchasing.PurchaseOrderDetail  
WHERE DueDate < '20020701';  
GO  
```  
  
 Se você precisar usar TOP para excluir linhas em uma ordem cronológica significativa, será preciso usar TOP junto com ORDER BY em uma instrução de subseleção. A consulta a seguir exclui as 10 linhas da tabela `PurchaseOrderDetail` que têm as primeiras datas de vencimento. Para garantir que apenas 10 linhas sejam excluídas, a coluna especificada na instrução de subseleção (`PurchaseOrderID`) é a chave primária da tabela. O uso de uma coluna não chave na instrução de subseleção pode resultar na exclusão de mais de 10 linhas se a coluna especificada contiver valores duplicados.  
  
```sql
DELETE FROM Purchasing.PurchaseOrderDetail  
WHERE PurchaseOrderDetailID IN  
   (SELECT TOP 10 PurchaseOrderDetailID   
    FROM Purchasing.PurchaseOrderDetail   
    ORDER BY DueDate ASC);  
GO  
```  
  
###  <a name="RemoteTables"></a> Excluindo linhas de uma tabela remota  
 Os exemplos nesta seção demonstram como excluir linhas de uma tabela de remota usando um [servidor vinculado](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) ou uma [função de conjunto de linhas](../../t-sql/functions/rowset-functions-transact-sql.md) para referenciar a tabela remota. Uma tabela remota existe em um servidor diferente ou em uma instância do SQL Server.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
#### <a name="f-deleting-data-from-a-remote-table-by-using-a-linked-server"></a>F. Excluindo dados de uma tabela remota por meio de um servidor vinculado  
 O exemplo a seguir exclui uma linhas de uma tabela remota. O exemplo começa criando um link com a fonte de dados remota usando [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). O nome do servidor vinculado, `MyLinkServer`, é especificado, em seguida, como parte do nome de objeto de quatro partes no formulário *server.catalog.schema.object*.  
  
```sql
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' or 'server_name\instance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  
```  
  
```sql
-- Specify the remote data source using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
DELETE MyLinkServer.AdventureWorks2012.HumanResources.Department 
WHERE DepartmentID > 16;  
GO  
```  
  
#### <a name="g-deleting-data-from-a-remote-table-by-using-the-openquery-function"></a>G. Excluindo dados de uma tabela remota por meio da função OPENQUERY  
 O exemplo a seguir exclui linhas de uma tabela remota especificando a função do conjunto de linhas [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) . O nome de servidor vinculado criado no exemplo anterior é usado neste exemplo.  
  
```sql
DELETE OPENQUERY (MyLinkServer, 'SELECT Name, GroupName 
FROM AdventureWorks2012.HumanResources.Department  
WHERE DepartmentID = 18');  
GO  
```  
  
#### <a name="h-deleting-data-from-a-remote-table-by-using-the-opendatasource-function"></a>H. Excluindo dados de uma tabela remota por meio da função OPENDATASOURCE  
 O exemplo a seguir exclui linhas de uma tabela remota especificando a função do conjunto de linhas [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md). Especifique um nome do servidor válido para a fonte de dados usando o formato *server_name* ou *server_name\instance_name*.  
  
```sql
DELETE FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source= <server_name>; Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department   
WHERE DepartmentID = 17;'  
```  
  
###  <a name="CaptureResults"></a> Capturando os resultados da instrução DELETE  
  
#### <a name="i-using-delete-with-the-output-clause"></a>I. Usando DELETE com a cláusula OUTPUT  
 O exemplo a seguir mostra como salvar os resultados de uma instrução `DELETE` em uma variável de tabela no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql
DELETE Sales.ShoppingCartItem  
OUTPUT DELETED.*   
WHERE ShoppingCartID = 20621;  
  
--Verify the rows in the table matching the WHERE clause have been deleted.  
SELECT COUNT(*) AS [Rows in Table] 
FROM Sales.ShoppingCartItem 
WHERE ShoppingCartID = 20621;  
GO  
```  
  
#### <a name="j-using-output-with-fromtablename-in-a-delete-statement"></a>J. Usando OUTPUT com <do_nome_da_tabela> em uma instrução DELETE  
 O exemplo a seguir exclui linhas da tabela `ProductProductPhoto` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] com base em critérios de pesquisa definidos na cláusula `FROM` da instrução `DELETE`. A cláusula `OUTPUT` retorna colunas da tabela que está sendo excluída, `DELETED.ProductID`, `DELETED.ProductPhotoID`, e colunas da tabela `Product` . É usada na cláusula `FROM` para especificar as linhas a serem excluídas.  
  
```sql
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="k-delete-all-rows-from-a-table"></a>K. Excluir todas as linhas de uma tabela  
 O exemplo a seguir exclui todas as linhas de uma tabela `Table1` porque uma cláusula WHERE não é usada para limitar o número de linhas excluídas.  
  
```sql
DELETE FROM Table1;  
```  
  
### <a name="l-delete-a-set-of-rows-from-a-table"></a>L. Excluir um conjunto de linhas de uma tabela com DELETE  
 O exemplo a seguir exclui todas as linhas do `Table1` tabela que tem um valor maior que 1.000,00 na coluna `StandardCost`.  
  
```sql
DELETE FROM Table1  
WHERE StandardCost > 1000.00;  
```  
  
### <a name="m-using-label-with-a-delete-statement"></a>M. Usando LABEL com uma instrução DELETE  
 O exemplo a seguir usa um rótulo com a instrução DELETE.  
  
```sql
DELETE FROM Table1  
OPTION ( LABEL = N'label1' );  
  
```  
  
### <a name="n-using-a-label-and-a-query-hint-with-the-delete-statement"></a>N. Usando um rótulo e uma dica de consulta com a instrução DELETE  
 Essa consulta mostra a sintaxe básica para uso de uma dica de consulta de junção com a instrução DELETE. Para obter mais informações sobre dicas de junção e como usar a cláusula OPTION, consulte [OPTION (SQL Server PDW)](https://msdn.microsoft.com/72bbce98-305b-42fa-a19f-d89620621ecc).  
  
```sql
-- Uses AdventureWorks  
  
DELETE FROM dbo.FactInternetSales  
WHERE ProductKey IN (   
    SELECT T1.ProductKey FROM dbo.DimProduct T1   
    JOIN dbo.DimProductSubcategory T2  
    ON T1.ProductSubcategoryKey = T2.ProductSubcategoryKey  
    WHERE T2.EnglishProductSubcategoryName = 'Road Bikes' )  
OPTION ( LABEL = N'CustomJoin', HASH JOIN ) ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [TRUNCATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)  
  
  

