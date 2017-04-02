---
title: "Criar exibi&#231;&#245;es indexadas | Microsoft Docs"
ms.custom: ""
ms.date: "05/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-views"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exibições indexadas [SQL Server], criando"
  - "exibições indexadas, exibições"
  - "instrução CREATE INDEX"
  - "opção large_value_types_out_of_row"
  - "exibições indexadas [SQL Server]"
  - "exibições [SQL Server], exibições indexadas"
ms.assetid: f86dd29f-52dd-44a9-91ac-1eb305c1ca8d
caps.latest.revision: 79
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 79
---
# Criar exibi&#231;&#245;es indexadas
  Este tópico descreve como criar uma exibição indexada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]. O primeiro índice criado em uma exibição deve ser um índice clusterizado exclusivo. Depois que o índice clusterizado exclusivo for criado, você poderá criar mais índices não clusterizados. Criar um índice clusterizado exclusivo em uma exibição melhora o desempenho da consulta porque a exibição é armazenada no banco de dados da mesma forma que uma tabela com um índice clusterizado é armazenada. O otimizador de consulta pode usar exibições indexadas para acelerar a execução da consulta. A exibição não precisa estar referenciada na consulta para o otimizador considerá-la para uma substituição.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 As seguintes etapas são necessárias para criar uma exibição indexada e são essenciais para o êxito da implementação da exibição indexada:  
  
1.  Verifique se as opções SET estão corretas para todas as tabelas existentes que serão referenciadas na exibição.  
  
2.  Verifique se as opções SET da sessão estão definidas corretamente antes de criar qualquer tabela nova e a exibição.  
  
3.  Verifique se a definição de exibição é determinística.  
  
4.  Crie a exibição usando a opção WITH SCHEMABINDING.  
  
5.  Crie o índice clusterizado exclusivo na exibição.  
  
###  <a name="Restrictions"></a> Opções SET necessárias para exibições indexadas  
 A avaliação da mesma expressão poderá produzir resultados diferentes no [!INCLUDE[ssDE](../../includes/ssde-md.md)] quando houver diferentes opções SET ativas durante a execução da consulta. Por exemplo, depois que a opção SET CONCAT_NULL_YIELDS_NULL for definida como ON, a expressão **'**abc**'** + NULL retornará o valor NULL. Entretanto, depois que CONCAT_NULL_YIEDS_NULL for definido como OFF, a mesma expressão produzirá **'**abc**'**.  
  
 Para verificar se as exibições podem ser mantidas corretamente e retornar resultados consistentes, as exibições indexadas requerem valores fixos para várias opções SET. As opções SET da seguinte tabela devem ser definidas com os valores mostrados na coluna **Valor Obrigatório** sempre que ocorrerem as seguintes condições:  
  
-   A exibição e os índices subsequentes são criados na exibição.  
  
-   As tabelas base referenciadas na exibição quando a tabela é criada.  
  
-   Houver qualquer operação de inserção, atualização ou exclusão executada em qualquer tabela que participe da exibição indexada. Esse requisito inclui operações como cópia em massa, replicação e consultas distribuídas.  
  
-   A exibição indexada for usada pelo otimizador de consulta para produzir o plano de consulta.  
  
    |opções SET|Valor necessário|Valor do servidor padrão|Padrão<br /><br /> Valor OLE DB e ODBC|Padrão<br /><br /> Valor da DB-Library|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|  
  
     *Definir ANSI_WARNINGS como ON define implicitamente ARITHABORT como ON.  
  
 Se você estiver usando uma conexão de servidor OLE DB ou ODBC, o único valor que deve ser modificado é a configuração ARITHABORT. Todos os valores DB-Library devem ser definidos corretamente no nível do servidor usando **sp_configure** ou no aplicativo usando o comando SET.  
  
> [!IMPORTANT]  
>  É altamente recomendável que você defina a opção de usuário ARITHABORT para ON no nível do servidor assim que a primeira exibição indexada ou o índice em uma coluna computada for criado em qualquer banco de dados no servidor.  
  
### Exibições determinísticas  
 A definição de uma exibição indexada deve ser determinística. Uma exibição será determinística se todas as expressões na lista selecionada, bem como as cláusulas WHERE e GROUP BY, forem determinísticas. As expressões determinísticas sempre retornam o mesmo resultado sempre que são avaliadas com um conjunto específico de valores de entrada. Somente as funções determinísticas podem participar de expressões determinísticas. Por exemplo, a função DATEADD é determinística porque sempre retorna o mesmo resultado para qualquer conjunto específico de valores de argumento para seus três parâmetros. GETDATE não é determinística porque sempre é invocada com o mesmo argumento, mas o valor que ela retorna é alterado a cada execução.  
  
 Para determinar se uma coluna de exibição é determinística, use a propriedade **IsDeterministic** da função [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) . Para determinar se uma coluna determinística em uma exibição com associação de esquema é precisa, use a propriedade **IsPrecise** da função COLUMNPROPERTY. COLUMNPROPERTY retornará 1 se for TRUE, 0 se for FALSE e NULL para entrada inválida. Isso significa que a coluna não é determinística ou não é precisa.  
  
 Mesmo que uma expressão seja determinística, se ela contiver expressões flutuantes, o resultado exato poderá depender da arquitetura do processador ou da versão de microcódigo. Para assegurar a integridade dos dados, tais expressões podem participar somente como colunas não chave de exibições indexadas. As expressões determinísticas que não contêm expressões flutuantes são chamadas de precisas. Somente as expressões determinísticas precisas podem participar de colunas de chave e de cláusulas WHERE ou GROUP BY de exibições indexadas.  
  
> [!NOTE]  
>  Não há suporte para exibições indexadas em consultas temporais (consultas que usam a cláusula **FOR SYSTEM_TIME**)  
  
### Requisitos adicionais  
 Além das opções SET e dos requisitos de função determinística, os seguintes requisitos devem ser atendidos:  
  
-   O usuário que executa CREATE INDEX deve ser o proprietário da exibição.  
  
-   Quando você cria o índice, a opção IGNORE_DUP_KEY deve ser definida como OFF (a configuração padrão).  
  
-   As tabelas devem ser referenciadas por meio de nomes de duas partes, *schema***.***tablename* na definição da exibição.  
  
-   Funções definidas pelo usuário referenciadas na exibição devem ser criadas usando a opção WITH SCHEMABINDING.  
  
-   Qualquer função definida pelo usuário referenciada na exibição deve ser referenciada por nomes de duas partes, *esquema***.***função*.  
  
-   A propriedade de acesso de dados de uma função definida pelo usuário deve ser NO SQL e a propriedade de acesso externa deve ser NO.  
  
-   Funções CLR (Common Language Runtime) podem aparecer na lista de seleção da exibição, mas não podem ser parte da definição de uma chave de índice clusterizado. Funções CLR não podem aparecer na cláusula WHERE da exibição ou na cláusula ON de uma operação JOIN na exibição.  
  
-   Funções CLR e métodos de tipos CLR definidos pelo usuário usados na definição da exibição devem ter as propriedades definidas como mostradas na tabela a seguir.  
  
    |Propriedade|Observação|  
    |--------------|----------|  
    |DETERMINISTIC = TRUE|Deve ser declarado explicitamente como um atributo do método do Microsoft .NET Framework.|  
    |PRECISE = TRUE|Deve ser declarado explicitamente como um atributo do método do .NET Framework.|  
    |DATA ACCESS = NO SQL|Determinado pela definição do atributo DataAccess para DataAccessKind.None e do atributo SystemDataAccess para SystemDataAccessKind.None.|  
    |EXTERNAL ACCESS = NO|Essa propriedade padroniza como NO rotinas CLR.|  
  
-   A exibição deve ser criada usando a opção WITH SCHEMABINDING.  
  
-   A exibição deve referenciar apenas as tabelas base que estão no mesmo banco de dados que a exibição. A exibição não pode fazer referência a outras exibições.  
  
-   A instrução SELECT na definição da exibição não deve conter os seguintes elementos do Transact-SQL:  
  
    ||||  
    |-|-|-|  
    |COUNT|Funções ROWSET (OPENDATASOURCE, OPENQUERY, OPENROWSET, AND OPENXML)|junções OUTER (LEFT, RIGHT ou FULL)|  
    |Tabela derivada (definida especificando uma instrução SELECT na cláusula FROM)|Autojunções|Especificando colunas usando SELECT \* ou SELECT *table_name*.*|  
    |DISTINCT|STDEV, STDEVP, VAR, VARP ou AVG|CTE (expressão de tabela comum)|  
    |colunas **float**\*, **text**, **ntext**, **image**, **XML** ou **filestream**|Subconsulta|Cláusula OVER, que inclui funções de classificação ou de janela de agregação|  
    |Predicados de texto completo (CONTAIN, FREETEXT).|Função SUM que referencia uma expressão que permite valor nulo|ORDER BY|  
    |Função de agregação CLR definida pelo usuário|INÍCIO|Operadores CUBE, ROLLUP ou GROUPING SETS|  
    |MIN, MAX|Operadores UNION, EXZip CodeT ou INTERSECT|TABLESAMPLE|  
    |Variáveis de tabela|OUTER APPLY ou CROSS APPLY|PIVOT, UNPIVOT|  
    |Conjuntos de colunas esparsas|Funções embutidas ou com valor de tabela de várias instruções|OFFSET|  
    |CHECKSUM_AGG|||  
  
     \*A exibição indexada pode conter colunas **float**; porém, essas colunas não podem ser incluídas na chave de índice clusterizado.  
  
-   Se GROUP BY estiver presente, a definição VIEW deverá conter COUNT_BIG(*) e não deverá conter HAVING. Essas restrições GROUP BY são aplicáveis apenas à definição de exibição indexada. Uma consulta pode usar uma exibição indexada em seu plano de execução mesmo que não satisfaça essas restrições GROUP BY.  
  
-   Se a definição de exibição contiver uma cláusula GROUP BY, a chave de índice clusterizado exclusivo poderá referenciar somente as colunas especificadas na cláusula GROUP BY.  
  
###  <a name="Recommendations"></a> Recomendações  
 Quando você referencia os literais de cadeia de caracteres **datetime** e **smalldatetime** em exibições indexadas, é recomendável converter explicitamente o literal para o tipo de data desejado, usando um estilo de formato de data determinístico. Para obter uma lista de estilos de formato de data determinísticos, veja [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md). Expressões que envolvem a conversão implícita de cadeias de caracteres para **datetime** or **smalldatetime** são consideradas não determinísticas. Isso ocorre porque os resultados dependem das configurações de LANGUAGE e DATEFORMAT da sessão de servidor. Por exemplo, os resultados da expressão `CONVERT (datetime, '30 listopad 1996', 113)` dependem da configuração LANGUAGE porque a cadeia de caracteres '`listopad`' significa meses diferentes em idiomas. Semelhantemente, na expressão `DATEADD(mm,3,'2000-12-01')`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta a cadeia de caracteres `'2000-12-01'` com base na configuração DATEFORMAT.  
  
 A conversão implícita de dados de caracteres não Unicode entre agrupamentos também é considerada não determinística.  
  
###  <a name="Considerations"></a> Considerações  
 A configuração da opção **large_value_types_out_of_row** de colunas em uma exibição indexada é herdada da configuração da coluna correspondente na tabela base. Esse valor é definido usando [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). A configuração padrão para colunas formadas de expressões é 0. Isso significa que tipos de valor grandes são armazenados na linha.  
  
 As exibições indexadas podem ser criadas em uma tabela particionada e elas próprias podem ser particionadas.  
  
 Para impedir que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] use exibições indexadas, inclua a dica OPTION (EXPAND VIEWS) na consulta. Além disso, se qualquer uma das opções listadas for definida incorretamente, isso evitará que o otimizador use os índices nas exibições. Para obter mais informações sobre a dica OPTION (EXPAND VIEWS), veja [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
 Todos os índices em uma exibição são descartados quando a exibição é descartada. Todos os índices não clusterizados e estatísticas criadas automaticamente na exibição são descartados quando o índice clusterizado é descartado. As estatísticas criadas pelo usuário na exibição são mantidas. Os índices não clusterizados podem ser descartados individualmente. Descartar o índice clusterizado na exibição remove o conjunto de resultados armazenado e o otimizador retorna para processar a exibição como se fosse uma exibição padrão.  
  
 Índices em tabelas e exibições podem ser desabilitados. Quando um índice clusterizado em uma tabela for desabilitado, os índices em exibições associadas à tabela também serão desabilitados.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão CREATE VIEW no banco de dados e a permissão ALTER no esquema no qual a exibição está sendo criada.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para criar uma exibição indexada  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria uma exibição e um índice nessa exibição. Duas consultas que usam a exibição indexada são incluídas.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Set the options to support indexed views.  
    SET NUMERIC_ROUNDABORT OFF;  
    SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
        QUOTED_IDENTIFIER, ANSI_NULLS ON;  
    GO  
    --Create view with schemabinding.  
    IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
    DROP VIEW Sales.vOrders ;  
    GO  
    CREATE VIEW Sales.vOrders  
    WITH SCHEMABINDING  
    AS  
        SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
            OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
        FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
        WHERE od.SalesOrderID = o.SalesOrderID  
        GROUP BY OrderDate, ProductID;  
    GO  
    --Create an index on the view.  
    CREATE UNIQUE CLUSTERED INDEX IDX_V1   
        ON Sales.vOrders (OrderDate, ProductID);  
    GO  
    --This query can use the indexed view even though the view is   
    --not specified in the FROM clause.  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
        OrderDate, ProductID  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND ProductID BETWEEN 700 and 800  
            AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
    GROUP BY OrderDate, ProductID  
    ORDER BY Rev DESC;  
    GO  
    --This query can use the above indexed view.  
    SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND DATEPART(mm,OrderDate)= 3  
            AND DATEPART(yy,OrderDate) = 2002  
    GROUP BY OrderDate  
    ORDER BY OrderDate ASC;  
    GO  
    ```  
  
 Para obter mais informações, veja [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
## Consulte também  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  