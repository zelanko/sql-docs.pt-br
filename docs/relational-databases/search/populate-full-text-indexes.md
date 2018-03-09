---
title: "Preencher índices de texto completo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index populations [full-text search]
- incremental populations [full-text search]
- populations [full-text search]
- full-text search [SQL Server], populations
- crawls [full-text search]
- automatic full-text index updates
- change tracking-based populations [full-text search]
- manual updates [full-text search]
- manual populations [full-text search]
- auto populations [full-text search]
- full-text indexes [SQL Server], key column
- full populations [full-text search]
- full-text indexes [SQL Server], populations
ms.assetid: 76767b20-ef55-49ce-8dc4-e77cb8ff618a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c139299c1613bb3d76328097fd1235f67ebe121a
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2018
---
# <a name="populate-full-text-indexes"></a>Popular índices de texto completo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
A criação e a manutenção de um índice de texto completo envolvem popular o índice usando um processo chamado *população* (também conhecido como *rastreamento*).  
  
##  <a name="types"></a> Types of population  
Um índice de texto completo dá suporte aos seguintes tipos de população:
-   População **completa**
-   População automática ou manual com base em **controle de alterações**
-   População incremental com base em um **carimbo de data/hora**
  
## <a name="full-population"></a>População completa  
 Durante uma população completa, entradas de índice são criadas para todas as linhas de uma tabela ou exibição indexada. Uma população completa de um índice de texto completo cria entradas de índice para todas as linhas da tabela base ou da exibição indexada.  
  
Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] popula totalmente um novo índice de texto completo assim que ele é criado.
-   Por um lado, uma população completa pode consumir uma quantidade significativa de recursos. Portanto, quando você criar um índice de texto completo durante períodos de pico, uma prática recomendada será atrasar a população completa até uma hora fora do horário de pico, principalmente se a tabela base de um índice de texto completo for grande.
-   Por outro lado, o catálogo de texto completo ao qual pertence o índice não é utilizável até que todos os seus índices de texto completo sejam preenchidos.

Para criar um índice de texto completo sem populá-lo imediatamente, especifique a `CHANGE_TRACKING OFF, NO POPULATION` cláusula na instrução `CREATE FULLTEXT INDEX`. Se você especificar `CHANGE_TRACKING MANUAL`, o mecanismo de texto completo não populará o novo índice de texto completo até que você execute uma instrução `ALTER FULLTEXT INDEX` usando a cláusula `START FULL POPULATION` ou `START INCREMENTAL POPULATION`. 

### <a name="example---create-a-full-text-index-without-running-a-full-population"></a>Exemplo – criar um índice de texto completo sem executar uma população completa  
 O exemplo a seguir cria um índice de texto completo na tabela `Production.Document` do banco de dados de exemplo `AdventureWorks` . Este exemplo usa `WITH CHANGE_TRACKING OFF, NO POPULATION` para atrasar a população completa inicial.  
  
```sql
CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
CREATE FULLTEXT CATALOG AW_Production_FTCat;  
CREATE FULLTEXT INDEX ON Production.Document  
(  
    Document                         --Full-text index column name   
        TYPE COLUMN FileExtension    --Name of column that contains file type information  
        Language 1033                 --1033 is LCID for the English language  
)  
    KEY INDEX ui_ukDoc  
    ON AW_Production_FTCat  
    WITH CHANGE_TRACKING OFF, NO POPULATION;  
GO  
  
```  
  
### <a name="example---run-a-full-population-on-a-table"></a>Exemplo – executar uma população completa em uma tabela  
 O exemplo a seguir executa uma população completa na tabela `Production.Document` do banco de dados de exemplo `AdventureWorks` .  
  
```sql
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
   
## <a name="population-based-on-change-tracking"></a>População com base em controle de alterações
 Como opção, você pode usar o controle de alterações para manter um índice de texto completo após a população completa inicial. Há uma pequena sobrecarga associada ao controle de alterações porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém uma tabela em que controla as alterações feitas na tabela base desde a última população. Quando você usa o controle de alterações, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém um registro das linhas na tabela base ou na exibição indexada que foram modificadas por atualizações, exclusões ou inserções. As alterações nos dados feitas por meio de WRITETEXT e UPDATETEXT não são refletidas no índice de texto completo e não são coletadas pelo controle de alterações.  
  
> [!NOTE]  
>  Para as tabelas que contêm uma coluna **carimbo de data/hora**, você pode usar a população incremental em vez do controle de alterações.  
  
 Quando você habilita o controle de alterações durante a criação do índice, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] popula completamente o novo índice de texto completo imediatamente após sua criação. Consequentemente, as alterações são controladas e propagadas para o índice de texto completo.

### <a name="enable-change-tracking"></a>Habilitar o controle de alterações
Há dois tipos de controle de alterações:
-   Automático (opção `CHANGE_TRACKING AUTO`). O controle de alterações automático é o comportamento padrão.
-   Manual (opção `CHANGE_TRACKING MANUAL`).   
  
 O tipo de controle de alterações determina como o índice de texto completo é populado, como segue:  
  
-   **População automática**  
  
     Por padrão ou se você especificar `CHANGE_TRACKING AUTO`, o mecanismo de texto completo usa a população automática no índice de texto completo. Depois que a população completa inicial é concluída, as alterações são controladas à medida que os dados são modificados na tabela base, e as alterações controladas são propagadas automaticamente. O índice de texto completo é atualizado em segundo plano, mas as alterações propagadas podem não ser refletidas imediatamente no índice.  
  
     **Para iniciar o controle de alterações com população automática**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING AUTO  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING AUTO  
  
    **Exemplo -– alterar um índice de texto completo para usar o controle de alterações automático**  
    O exemplo a seguir altera o índice de texto completo da tabela `HumanResources.JobCandidate` do banco de dados de exemplo `AdventureWorks` para usar o controle de alterações com população automática.  
  
    ```sql  
    USE AdventureWorks;  
    GO  
    ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
    GO   
    ```  
  
-   **População manual**  
  
     Se você especificar CHANGE_TRACKING MANUAL, o Mecanismo de Texto Completo usará população manual no índice de texto completo. Depois que a população completa inicial é concluída, as alterações são controladas à medida que os dados são modificados na tabela base. Porém, eles não serão propagados para o índice de texto completo até que você execute uma instrução ALTER FULLTEXT INDEX… Instrução START UPDATE POPULATION . É possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para chamar essa instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] periodicamente.  
  
     **Para começar a controlar alterações com população manual**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING MANUAL  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING MANUAL  
  
    **Exemplo – criar um índice de texto completo com controle de alterações manual**  
    O exemplo a seguir cria um índice de texto completo que usará o controle de alterações com população manual na tabela `HumanResources.JobCandidate` do banco de dados de exemplo `AdventureWorks` .  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
    CREATE FULLTEXT CATALOG ft AS DEFAULT;  
    CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
       KEY INDEX ui_ukJobCand   
       WITH CHANGE_TRACKING=MANUAL;  
    GO  
    ```  
  
    **Exemplo – executar uma população manual**  
    O exemplo a seguir executa uma população manual no índice de texto completo com controle de alterações da tabela `HumanResources.JobCandidate` do banco de dados de exemplo `AdventureWorks` .  
  
    ```sql 
    USE AdventureWorks;  
    GO  
    ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
    GO  
    ```
   
### <a name="disable-change-tracking"></a>Desabilitar o controle de alterações 
  
-   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING OFF  
  
-   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING OFF  
   
  
## <a name="incremental-population-based-on-a-timestamp"></a>População incremental com base em um carimbo de data/hora  
 Uma população incremental é um mecanismo alternativo para popular um índice de texto completo manualmente. Se uma tabela tiver um volume alto de inserções, usar a população incremental poderá ser mais eficiente do que usar a população manual.
 
 Você pode executar uma população incremental para um índice de texto completo que tem CHANGE_TRACKING definido como MANUAL ou OFF. 
  
 O requisito para população incremental é que a tabela indexada deve ter uma coluna do tipo de dados **timestamp** . Se uma coluna **timestamp** não existir, a população incremental não poderá ser executada.   

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a coluna **timestamp** para identificar linhas que foram alteradas desde a última população. A população incremental então atualiza o índice de texto completo com linhas adicionadas, excluídas ou modificadas após a última população ou enquanto a última população estava em andamento. Ao término de uma população, o Mecanismo de Texto Completo registra um novo valor de **timestamp** . Esse valor é o maior valor de **carimbo de data/hora** que o SQL Gatherer encontrou. Esse valor será usado quando a próxima população incremental for iniciada.  
 
Em alguns casos, a solicitação de uma população incremental resulta em uma população completa.
-   Uma solicitação para população incremental em uma tabela sem uma coluna **timestamp** resulta em uma operação de população completa.
-   Se a primeira população em um índice de texto completo for uma população incremental, ele indexará todas as linhas, tornando-a equivalente a uma população completa. 
-   Se nenhum metadado que afete o índice de texto completo da tabela for alterado desde a última população, as solicitações de população incremental serão implementadas como populações completas. Isso inclui alterações de metadados geradas pela alteração de qualquer coluna, índice ou definições de índice de texto completo. 

### <a name="run-an-incremental-population"></a>Executar uma população incremental
  
 Para executar uma população incremental, execute uma instrução `ALTER FULLTEXT INDEX` usando a cláusula `START INCREMENTAL POPULATION`.  
  
###  <a name="create"></a> Criar ou alterar uma agenda de população incremental   
  
1.  No Management Studio, no Pesquisador de Objetos, expanda o servidor.  
  
2.  Expanda **Bancos de Dados**e expanda o banco de dados que contém o índice de texto completo.  
  
3.  Expanda **Tabelas**.  
  
    Clique com o botão direito do mouse na tabela em que o índice de texto completo está definido, selecione **Índice de Texto Completo**e, no menu de contexto **Índice de Texto Completo** , clique em **Propriedades**. Este procedimento abre a caixa de diálogo **Propriedades do Índice de Texto Completo** .  

    > [!IMPORTANT]  
    >  Se a tabela base ou a exibição não contiverem uma coluna com o tipo de dados **carimbo de data/hora**, a população incremental não será possível.
      
1.  No painel **Selecionar uma página**, selecione **Agendas**.  
  
     Use esta página para criar ou gerenciar agendas para um trabalho do SQL Server Agent que inicia uma população incremental de tabela na tabela base ou na exibição indexada do índice de texto completo.  

     As opções são as seguintes:  
  
    -   Para **criar** uma nova agenda, clique em **Novo**.  
  
        Este procedimento abre a caixa de diálogo **Novo Agendamento da Tabela de Indexação de Texto Completo** , em que é possível criar um agendamento. Para salvar o agendamento, clique em **OK**.  
  
        > [!IMPORTANT]  
        >  Um trabalho do SQL Server Agent (Iniciar População Incremental da Tabela em *database_name*.*table_name*) é associado a um novo agendamento depois que você sai da caixa de diálogo **Propriedades do Índice de Texto Completo** . Se você criar várias agendas para o mesmo índice de texto completo, todas elas usarão o mesmo trabalho.  
  
    -   Para **alterar** uma agenda existente, selecione a agenda existente e clique em **Editar**.  
  
         Este procedimento abre a caixa de diálogo **Novo Agendamento da Tabela de Indexação de Texto Completo** , em que é possível modificar o agendamento.  
  
        > [!NOTE]  
        >  Para obter informações sobre como modificar um trabalho do SQL Server Agent, consulte [Modify a Job](http://msdn.microsoft.com/library/dd5e5f20-20c4-4ab9-a19a-db87577dcd43) (Modificar um trabalho).  
  
    -   Para **remover** uma agenda existente, selecione a agenda existente e clique em **Excluir**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]   
  
##  <a name="crawl"></a> Solucionar erros em uma população de texto completo (rastreamento)  
Quando um erro ocorrer durante um rastreamento, o recurso de registro de rastreamento de pesquisa de texto completo cria e mantém um log de rastreamento, que é um texto sem-formatação. Cada log de rastreamento corresponde a um catálogo de texto completo específico. Por padrão, os logs de rastreamento para uma determinada instância (no exemplo, a instância padrão) estão localizados na pasta `%ProgramFiles%\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\LOG`.
 
O arquivo de log de rastreamento segue o seguinte esquema de nomeação:  
  
`SQLFT<DatabaseID><FullTextCatalogID>.LOG[<n>]`
  
As partes variáveis do nome do arquivo de log de rastreamento são as seguintes.
-   <**DatabaseID**> – a ID de um banco de dados. <**dbid**> é um número de cinco dígitos com zeros à esquerda.  
-   <**FullTextCatalogID**> – ID do catálogo de texto completo. <**catid**> é um número de cinco dígitos com zeros à esquerda.  
-   <**n**> – é um inteiro que indica que existe um ou mais logs de rastreamento do mesmo catálogo de texto completo.  
  
 Por exemplo, `SQLFT0000500008.2` é o arquivo de log de rastreamento de um banco de dados com a ID de banco de dados = 5 e a ID de catálogo de texto completo = 8. O 2 no final do nome do arquivo indica que há dois arquivos de log de rastreamento para esse par de banco de dados/catálogo.  

## <a name="see-also"></a>Consulte Também  
 [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)   
 [Iniciar a pesquisa de texto completo](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
