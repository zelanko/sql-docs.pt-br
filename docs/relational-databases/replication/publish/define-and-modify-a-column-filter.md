---
title: "Definir e modificar um filtro de colunas | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "filters [SQL Server replication], column"
  - "modifying filters, column"
  - "modifying filters"
  - "filtros de colunas [replicação do SQL Server]"
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# Definir e modificar um filtro de colunas
  Este tópico descreve como definir e modificar um filtro de colunas no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para definir e modificar um filtro de colunas, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Algumas colunas não podem ser filtradas; Para obter mais informações, consulte [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md). Se você modificar um filtro de coluna depois que as assinaturas forem inicializadas, será preciso gerar um novo instantâneo e reinicializar todas as assinaturas depois de fazer a alteração. Para obter mais informações sobre os requisitos para alterações de propriedade, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Defina filtros de coluna na página **Artigos** do Assistente para Nova Publicação. Para obter mais informações sobre como usar o Assistente para nova publicação, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md).  
  
 Definir e modificar filtros de coluna no **artigos** página o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre propriedades de artigo e publicação, consulte [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para definir um filtro de coluna  
  
1.  Na página **Artigos** do Assistente para Nova Publicação, expanda a tabela a ser filtrada no painel **Objetos para publicação** .  
  
2.  Desmarque a caixa de seleção próxima a cada coluna que você quer filtrar.  
  
#### Para modificar a filtragem de coluna  
  
1.  No **artigos** página do **Propriedades de publicação - \< publicação>** caixa de diálogo caixa, expanda a tabela a ser filtrada no **objetos para publicação** painel.  
  
2.  Desmarque a caixa de seleção próxima a cada coluna que você deseja filtrar e certifique-se de que a caixa de seleção esteja marcada para cada coluna que deve ser incluída no artigo.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Quando for criar artigos de tabela, você pode definir as colunas para serem incluídas no artigo e alterar as colunas após o artigo ter sido definido. Colunas filtradas podem ser criadas e modificadas de forma programada usando os procedimentos de replicação armazenados.  
  
> [!NOTE]  
>  Os procedimentos a seguir assumem que a tabela subjacente não tenha sido alterada. Para obter informações sobre como replicar alterações DDL (linguagem) de definição de dados para tabelas publicadas, consulte [fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
#### Para definir um filtro de coluna para um artigo publicado em um instantâneo ou publicação transacional  
  
1.  Defina o artigo a ser filtrado. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  No publicador do banco de dados de publicação, execute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md). Isto define as colunas a serem incluídas ou removidas do artigo.  
  
    -   Se publicar apenas algumas colunas de uma tabela com várias colunas, execute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna sendo adicionada. Especifique o nome de coluna para **@column** e um valor de **adicionar** para **@operation**.  
  
    -   Se publicar a maioria das colunas em uma tabela com várias colunas, execute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), especificando um valor de **nulo** para **@column** e um valor de **Adicionar** para **@operation** para adicionar todas as colunas. Em seguida, execute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), uma vez para cada coluna sendo excluída, especificando um valor de **drop** para **@operation** e o nome da coluna excluída para **@column**.  
  
3.  No publicador do banco de dados de publicação, execute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Especifique o nome da publicação para **@publication** e o nome do artigo filtrado para **@article**. Isto cria os objetos de sincronização para o artigo filtrado.  
  
#### Para alterar um filtro de coluna para incluir colunas adicionais no artigo publicado em um instantâneo ou em uma publicação transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna sendo adicionada. Especifique o nome de coluna para **@column** e um valor de **adicionar** para **@operation**.  
  
2.  No publicador do banco de dados de publicação, execute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Especifique o nome da publicação para **@publication** e o nome do artigo filtrado para **@article**. Se a publicação tiver assinaturas existentes, especifique um valor de **1** para **@change_active**. Isto cria novamente os objetos de sincronização para o artigo filtrado.  
  
3.  Execute novamente o Snapshot Agent da publicação para gerar um instantâneo atualizado.  
  
4.  Reinicialize as assinaturas. Para obter mais informações, consulte [reinicializar assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### Para alterar um filtro de coluna para remover colunas de um artigo publicado em um instantâneo ou em uma publicação transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) uma vez para cada coluna sendo removida. Especifique o nome de coluna para **@column** e um valor de **descartar** para **@operation**.  
  
2.  No publicador do banco de dados de publicação, execute [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Especifique o nome da publicação para **@publication** e o nome do artigo filtrado para **@article**. Se a publicação tiver assinaturas existentes, especifique um valor de **1** para **@change_active**. Isto cria novamente os objetos de sincronização para o artigo filtrado.  
  
3.  Execute novamente o Snapshot Agent da publicação para gerar um instantâneo atualizado.  
  
4.  Reinicialize as assinaturas. Para obter mais informações, consulte [reinicializar assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### Para definir um filtro de coluna para um artigo publicado em uma publicação de mesclagem  
  
1.  Defina o artigo a ser filtrado. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  No publicador do banco de dados de publicação, execute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md). Isto define as colunas a serem incluídas ou removidas do artigo.  
  
    -   Se publicar apenas algumas colunas de uma tabela com várias colunas, execute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) uma vez para cada coluna sendo adicionada. Especifique o nome de coluna para **@column** e um valor de **adicionar** para **@operation**.  
  
    -   Se publicar a maioria das colunas em uma tabela com várias colunas, execute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), especificando um valor de **nulo** para **@column** e um valor de **Adicionar** para **@operation** para adicionar todas as colunas. Em seguida, execute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), uma vez para cada coluna sendo excluída, especificando um valor de **drop** para **@operation** e o nome da coluna excluída para **@column**.  
  
#### Para alterar um filtro de coluna para incluir colunas adicionais no artigo publicado em uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) uma vez para cada coluna sendo adicionada. Especifique o nome da coluna **@column**, um valor de **Adicionar** para **@operation** e um valor de **1** para ambos **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
2.  Execute novamente o Snapshot Agent da publicação para gerar um instantâneo atualizado.  
  
3.  Reinicialize as assinaturas. Para obter mais informações, consulte [reinicializar assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
#### Para alterar um filtro de coluna para remover colunas de um artigo publicado em uma publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) uma vez para cada coluna sendo removida. Especifique o nome da coluna **@column**, um valor de **drop** para **@operation** e um valor de **1** para ambos **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
2.  Execute novamente o Snapshot Agent da publicação para gerar um instantâneo atualizado.  
  
3.  Reinicialize as assinaturas. Para obter mais informações, consulte [reinicializar assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md).  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Nesse exemplo de replicação transacional, a coluna `DaysToManufacture` é removida de um artigo com base na tabela `Product` .  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_1.sql)]  
  
 Nesse exemplo de replicação de mesclagem, a coluna `CreditCardApprovalCode` é removida de um artigo com base na tabela `SalesOrderHeader` .  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_2.sql)]  
  
## Consulte também  
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtrar dados publicados para replicação de mesclagem](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  