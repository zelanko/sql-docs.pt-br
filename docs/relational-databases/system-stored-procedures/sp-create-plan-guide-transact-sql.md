---
title: sp_create_plan_guide (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide
- sp_create_plan_guide_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_create_plan_guide
ms.assetid: 5a8c8040-4f96-4c74-93ab-15bdefd132f0
caps.latest.revision: "82"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70caae94a352f014757bd00099b43019c08f4a2c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spcreateplanguide-transact-sql"></a>sp_create_plan_guide (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma guia de plano associando dicas de consulta ou planos de consulta reais a consultas em um banco de dados. Para obter mais informações sobre guias de plano, consulte [Plan Guides](../../relational-databases/performance/plan-guides.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_create_plan_guide [ @name = ] N'plan_guide_name'  
    , [ @stmt = ] N'statement_text'  
    , [ @type = ] N'{ OBJECT | SQL | TEMPLATE }'  
    , [ @module_or_batch = ]  
      {   
                    N'[ schema_name. ] object_name'  
        | N'batch_text'  
        | NULL  
      }  
    , [ @params = ] { N'@parameter_name data_type [ ,...n ]' | NULL }   
    , [ @hints = ] { N'OPTION ( query_hint [ ,...n ] )'   
                 | N'XML_showplan'  
                 | NULL }  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @name =] N'*plan_guide_name*'  
 É o nome da guia de plano. Os nomes de guia de plano têm escopo no banco de dados atual. *plan_guide_name* devem estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md) e não pode começar com o sinal de número (#). O comprimento máximo de *plan_guide_name* é 124 caracteres.  
  
 [ @stmt =] N'*statement_text*'  
 É uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] para a qual deve ser criada um guia de plano. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consulta optimizer reconhece uma consulta que corresponde a *statement_text*, *plan_guide_name* entra em vigor. Para a criação de um guia de plano tenha êxito, *statement_text* devem aparecer no contexto especificado pelo @type, @module_or_batch, e @params parâmetros.  
  
 *statement_text* deve ser fornecido de forma que permite que o otimizador de consulta para correspondência com a instrução fornecida correspondente dentro do lote ou módulo identificado pelos @module_or_batch e @params. Para obter mais informações, consulte a seção “Comentários”. O tamanho de *statement_text* é limitado apenas pela memória disponível do servidor.  
  
 [@type =] N'{OBJETO | SQL | MODELO}'  
 É o tipo de entidade na qual *statement_text* é exibida. Isso especifica o contexto de correspondência *statement_text* para *plan_guide_name*.  
  
 OBJECT  
 Indica *statement_text* aparece no contexto de um [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimento armazenado, função escalar de uma função com valor de tabela com várias instruções, ou [!INCLUDE[tsql](../../includes/tsql-md.md)] gatilho DML no banco de dados atual.  
  
 SQL  
 Indica *statement_text* aparece no contexto de uma instrução ou lote autônomo que pode ser enviado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de qualquer mecanismo. [!INCLUDE[tsql](../../includes/tsql-md.md)]instruções enviadas por objetos common language runtime (CLR) ou procedimentos armazenados estendidos ou pelo uso de EXEC n' '*sql_string*', são processadas como lotes no servidor e, portanto, devem ser identificadas como @type  **=**  'SQL'. Se SQL for especificado, a dica de consulta PARAMETERIZATION {FORCED | SIMPLE} não pode ser especificado o @hints parâmetro.  
  
 TEMPLATE  
 Indica que o guia de plano se aplica a qualquer consulta que aplica parâmetros ao formulário indicado em *statement_text*. Se TEMPLATE for especificado, apenas o PARAMETERIZATION {FORCED | Dica de consulta simples} pode ser especificada no @hints parâmetro. Para obter mais informações sobre guias de plano TEMPLATE, consulte [especificar comportamento de parametrização de consulta com guias de plano usando](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md).  
  
 [@module_or_batch =] {N'[ *schema_name*. ] *object_name*' | N'*batch_text*' | NULL}  
 Especifica o nome do objeto no qual *statement_text* aparece, ou o texto de lote no qual *statement_text* é exibida. O texto de lote não pode incluir um uso*banco de dados* instrução.  
  
 Para obter um guia de plano corresponder a um lote enviado de um aplicativo, *batch_tex*deve ser fornecido no mesmo formato, caractere por caractere, que é enviado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhuma conversão interna é executada para facilitar essa correspondência. Para obter mais informações, consulte a seção Comentários.  
  
 [*schema_name*.] *object_name* Especifica o nome de um [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimento armazenado, função escalar de uma função com valor de tabela com várias instruções, ou [!INCLUDE[tsql](../../includes/tsql-md.md)] gatilho DML que contém *statement_text*. Se *schema_name* não for especificado, *schema_name* usa o esquema do usuário atual. Se NULL for especificado e @type = 'SQL', o valor de @module_or_batch é definido como o valor de @stmt. Se @type = ' modelo**'**, @module_or_batch deve ser NULL.  
  
 [ @params =] {N' *@parameter_name data_type* [,*... n* ]' | NULL}  
 Especifica as definições de todos os parâmetros que são inseridos em *statement_text*. @paramsaplica-se somente quando uma das seguintes opções for verdadeira:  
  
-   @type= 'SQL' ou 'TEMPLATE'. Se 'TEMPLATE' @params não deve ser NULL.  
  
-   *statement_text* é enviado usando sp_executesql e um valor para o @params parâmetro for especificado, ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envia internamente uma instrução depois de parametrizá-la. O envio de consultas com parâmetros de APIs de banco de dados (incluindo ODBC, OLE DB e ADO.NET) é exibido para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como chamadas para sp_executesql ou rotinas de cursor de servidor de API; portanto, a sua correspondência pode ser feita por guias de plano SQL ou TEMPLATE.  
  
 *@parameter_namedata_type* deve ser fornecido exatamente no mesmo formato que é enviado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando sp_executesql ou enviado internamente após parametrização. Para obter mais informações, consulte a seção Comentários. Se o lote não contiver parâmetros, NULL deverá ser especificado. O tamanho do @params é limitado apenas pela memória disponível no servidor.  
  
 [@hints =] {N'Option (*query_hint* [,*... n* ])' | N'*XML_showplan*' | NULL}  
 N'Option (*query_hint* [,*... n* ])  
 Especifica uma cláusula OPTION a anexar a uma consulta que corresponde a @stmt. @hints deve ser sintaticamente igual uma cláusula OPTION em uma instrução SELECT e pode conter qualquer sequência válida de dicas de consulta.  
  
 N'*XML_showplan*'  
 É o plano de consulta em formato XML a ser aplicado como dica.  
  
 Recomendamos atribuir o Plano de execução XML a uma variável; caso contrário, você deve inserir um escape para quaisquer aspas simples no Plano de execução colocando antes delas outra aspa simples. Consulte o exemplo E.  
  
 NULL  
 Indica que qualquer dica existente especificada na cláusula OPTION da consulta não é aplicada à consulta. Para obter mais informações, consulte [cláusula OPTION &#40; Transact-SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Os argumentos para sp_create_plan_guide devem ser fornecidos na ordem em que aparecem. Quando você fornece valores para os parâmetros de **sp_create_plan_guide**, todos os nomes de parâmetros devem ser especificados explicitamente ou nenhum deles deve ser especificado. Por exemplo, se **@name =** for especificado, então **@stmt =**, **@type =** e assim por diante, também deverá ser especificado. Da mesma forma, se **@name =** for omitido e apenas o valor do parâmetro for fornecido, os nomes de parâmetro restantes também deverão ser omitidos e apenas seus valores deverão ser fornecidos. Os nomes de argumento são usados apenas para fins descritivos, para ajudar compreender a sintaxe. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não verifica se o nome de parâmetro especificado corresponde ao nome do parâmetro na posição em que o nome é usado.  
  
 Você pode criar mais de um guia de plano OBJECT ou SQL para a mesma consulta e lote ou módulo. Porém, só um guia de plano pode ser ativado em um determinado momento.  
  
 Os guias de plano OBJECT não podem ser criados para um valor @module_or_batch que referencie um procedimento armazenado, uma função ou um gatilho DML que especifique a cláusula WITH ENCRYPTION ou que seja temporário.  
  
 A tentativa de cancelar ou modificar uma função, procedimento armazenado ou gatilho DML referenciado por um guia de plano, habilitado ou desabilitado, provoca um erro. A tentativa de descartar uma tabela com um gatilho definido nela que é mencionado por um guia de plano também causa um erro.  
  
> [!NOTE]  
>  Os guias de plano não podem ser usados em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md). As guias de plano são visíveis em qualquer edição. Também é possível anexar um banco de dados contendo guias de plano a qualquer edição. Os guias de plano permanecem intactos quando o banco de dados é restaurado ou anexado a uma versão atualizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você deve verificar a finalidade dos guias de plano em cada banco de dados depois de executar uma atualização de servidor.  
  
## <a name="plan-guide-matching-requirements"></a>Guia de plano correspondente a requisitos  
 Para guias de plano que especifiquem @type = 'SQL' ou @type = 'TEMPLATE' para corresponder com êxito de uma consulta, os valores para *batch_text* e  *@parameter_name data_type* [,*... n* ] deve ser fornecido exatamente no mesmo formato que seus equivalentes enviados pelo aplicativo. Isso significa você deve fornecer o texto de lote exatamente como o compilador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o recebe. Para capturar o lote real e texto de parâmetro, você pode usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Para obter mais informações, consulte [usar o SQL Server Profiler para criar e testar guias de plano](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md).  
  
 Quando @type = 'SQL' e @module_or_batch forem definidos como NULL, o valor @module_or_batch será definido com o valor @stmt. Isso significa que o valor de *statement_text* deve ser fornecido exatamente no mesmo formato, caractere por caractere, que é enviado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhuma conversão interna é executada para facilitar essa correspondência.  
  
 Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corresponde ao valor do *statement_text* para *batch_text* e  *@parameter_name data_type* [,*... n* ], ou Se @type = **'**objeto ', para o texto da consulta correspondente em *object_name*, os seguintes elementos de cadeia de caracteres não são considerados:  
  
-   Caracteres de espaço em branco (guias, espaços, retornos de carro ou alimentações de linha) dentro da cadeia de caracteres.  
  
-   Comentários ( **--**  ou  **/ \* \* /** ).  
  
-   Ponto-e-vírgulas à direita  
  
 Por exemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode corresponder a *statement_text* cadeia de caracteres `N'SELECT * FROM T WHERE a = 10'` à seguinte *batch_text*:  
  
 `N'SELECT *`  
  
 `FROM T`  
  
 `WHERE a=10'`  
  
 No entanto, a mesma cadeia de caracteres não deve corresponder a este *batch_text*:  
  
 `N'SELECT * FROM T WHERE b = 10'`  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignora o retorno de carro, a alimentação de linha e caracteres de espaço dentro da primeira consulta. Na segunda consulta, a sequência `WHERE b = 10` é interpretada diferentemente de `WHERE a = 10`. A correspondência diferencia maiúsculas de minúsculas e acentos (mesmo quando o agrupamento do banco de dados não diferencia), exceto no caso de palavras-chave, no qual não há diferenciação. A correspondência não diferencia maiúsculas de minúsculas em formas abreviadas de palavras-chave. Por exemplo, as palavras-chave `EXECUTE`, `EXEC` e `execute` são consideradas equivalentes.  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>Efeito do guia de plano no cache do esquema  
 Criar um guia de plano em um módulo remove o plano de consulta desse módulo do cache do esquema. Criar um guia de plano do tipo OBJECT ou SQL em um lote remove o plano de consulta de um lote que tem o mesmo valor de hash. Criar um guia de plano do tipo TEMPLATE remove todos os lotes da instrução única do cache do esquema dentro desse banco de dados.  
  
## <a name="permissions"></a>Permissões  
 A criação de um guia de plano do tipo OBJECT requer a permissão ALTER no objeto mencionado. A criação de um guia de plano do tipo SQL ou TEMPLATE requer a permissão ALTER no banco de dados atual.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-plan-guide-of-type-object-for-a-query-in-a-stored-procedure"></a>A. Criando um guia de plano do tipo OBJECT para uma consulta em um procedimento armazenado  
 O exemplo a seguir cria um guia de plano que faz a correspondência de uma consulta executada no contexto de um procedimento armazenado com base em aplicativo e aplica a dica `OPTIMIZE FOR` à consulta.  
  
 Aqui está o procedimento armazenado:  
  
```  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t   
        ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country_region;  
END  
GO  
```  
  
 Este é o guia de plano criado na consulta no procedimento armazenado:  
  
```  
EXEC sp_create_plan_guide   
    @name =  N'Guide1',  
    @stmt = N'SELECT *  
              FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.Customer AS c   
                 ON h.CustomerID = c.CustomerID  
              INNER JOIN Sales.SalesTerritory AS t   
                 ON c.TerritoryID = t.TerritoryID  
              WHERE t.CountryRegionCode = @Country_region',  
    @type = N'OBJECT',  
    @module_or_batch = N'Sales.GetSalesOrderByCountry',  
    @params = NULL,  
    @hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
### <a name="b-creating-a-plan-guide-of-type-sql-for-a-stand-alone-query"></a>B. Criando um guia de plano do tipo SQL para uma consulta autônoma  
 O exemplo a seguir cria um guia de plano que faz a correspondência de uma consulta em um lote enviado por um aplicativo que usa o procedimento armazenado do sistema sp_executesql.  
  
 Este é o lote:  
  
```  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 Para impedir que um plano de execução paralelo seja gerado nesta consulta, crie o seguinte guia de plano:  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT TOP 1 *   
              FROM Sales.SalesOrderHeader   
              ORDER BY OrderDate DESC',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (MAXDOP 1)';  
```  
  
### <a name="c-creating-a-plan-guide-of-type-template-for-the-parameterized-form-of-a-query"></a>C. Criando um guia de plano do tipo TEMPLATE para o formulário parametrizado de uma consulta  
 O exemplo a seguir cria um guia de plano que faz a correspondência de qualquer consulta com parâmetros com um formulário especificado, e direciona o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para forçar a aplicação de parâmetros da consulta. As duas consultas a seguir são sintaticamente equivalentes, mas só diferem nos valores literais constantes.  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 Este é o guia de plano na forma com parâmetros da consulta:  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 No exemplo anterior, o valor do parâmetro `@stmt` é a forma com parâmetros da consulta. O único modo confiável de obter esse valor para uso em sp_create_plan_guide é por meio do procedimento armazenado do sistema [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) . O script a seguir pode ser usado para obter a consulta parametrizada e, em seguida, criar um guia de plano para ela.  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  O valor das literais constantes do parâmetro `@stmt` passado para sp_get_query_template pode afetar o tipo de dados escolhido para o parâmetro que substitui a literal. Isso afetará a correspondência do guia de plano. Pode ser necessário criar mais de um guia de plano para lidar com diferentes intervalos de valores de parâmetros.  
  
### <a name="d-creating-a-plan-guide-on-a-query-submitted-by-using-an-api-cursor-request"></a>D. Criando um guia de plano em uma consulta enviada com o uso de uma solicitação de cursor API  
 Os guias de plano podem ser correspondentes a consultas enviadas das rotinas de cursor de servidor de API. Essas rotinas incluem sp_cursorprepare, sp_cursorprepexec e sp_cursoropen. Os aplicativos que usam APIs ADO, OLE DB e ODBC interagem frequentemente com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando cursores de servidor de API. É possível verificar a chamada das rotinas de cursor de servidor de API nos rastreamentos do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] por meio da exibição do evento de rastreamento do profiler RPC:Starting.  
  
 Suponha que os dados a seguir apareçam em um evento de rastreamento do profiler RPC:Starting para uma consulta que você deseja ajustar com um guia de plano:  
  
```  
DECLARE @p1 int;  
SET @p1=-1;  
DECLARE @p2 int;  
SET @p2=0;  
DECLARE @p5 int;  
SET @p5=4104;  
DECLARE @p6 int;  
SET @p6=8193;  
DECLARE @p7 int;  
SET @p7=0;  
EXEC sp_cursorprepexec @p1 output,@p2 output,N'@P1 varchar(255),@P2 varchar(255)',N'SELECT * FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID WHERE h.OrderDate BETWEEN @P1 AND @P2',@p5 OUTPUT,@p6 OUTPUT,@p7 OUTPUT,'20040101','20050101'  
SELECT @p1, @p2, @p5, @p6, @p7;  
```  
  
 Observe que o plano da consulta `SELECT` na chamada de `sp_cursorprepexec` está usando uma junção de mesclagem, mas você deseja usar uma junção de hash. A consulta enviada com o uso de `sp_cursorprepexec` tem parâmetros, incluindo uma cadeia de caracteres de consulta e outra de parâmetros. Você pode criar o seguinte guia de plano para alterar a opção de plano usando as cadeias de caracteres de consulta e de parâmetro exatamente como elas são exibidas, caractere por caractere, na chamada de `sp_cursorprepexec`.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'APICursorGuide',  
    @stmt = N'SELECT * FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.SalesOrderDetail AS d   
                ON h.SalesOrderID = d.SalesOrderID   
              WHERE h.OrderDate BETWEEN @P1 AND @P2',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = N'@P1 varchar(255),@P2 varchar(255)',  
    @hints = N'OPTION(HASH JOIN)';  
```  
  
 As execuções subsequentes dessa consulta pelo aplicativo serão afetadas por esse guia de plano, e uma junção de hash será usada para processar a consulta.  
  
### <a name="e-creating-a-plan-guide-by-obtaining-the-xml-showplan-from-a-cached-plan"></a>E. Criando um guia de plano por meio da obtenção do plano de execução XML de um plano em cache.  
 O exemplo a seguir cria um guia de plano para uma instrução SQL ad hoc simples. Especifique o XML Showplan para a consulta diretamente no parâmetro `@hints` para que o plano de consulta desejado para essa instrução seja fornecido no guia de plano. O exemplo executa a instrução SQL primeiro para gerar um plano no cache do esquema. Nesse exemplo, supõe-se que o plano gerado é o desejado e que nenhum ajuste de consulta adicional é necessário. O Plano de execução XML da consulta é obtido por meio da consulta das exibições de gerenciamento dinâmico `sys.dm_exec_query_stats`, `sys.dm_exec_sql_text`e `sys.dm_exec_text_query_plan` e é atribuído à variável `@xml_showplan` . Em seguida, a variável `@xml_showplan` é passada à instrução `sp_create_plan_guide` no parâmetro `@hints` . Também é possível criar um guia de plano com base em um plano de consulta no cache de plano por meio do procedimento armazenado [sp_create_plan_guide_from_handle](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md) .  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints =@xml_showplan;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Guias de plano](../../relational-databases/performance/plan-guides.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [Mecanismo de banco de dados armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.DM exec_sql_text &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.DM exec_query_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)   
 [sp_get_query_template &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md)  
  
  
