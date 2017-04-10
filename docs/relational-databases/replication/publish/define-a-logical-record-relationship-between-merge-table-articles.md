---
title: "Definir uma rela&#231;&#227;o de registro l&#243;gico entre artigos da tabela de mesclagem | Microsoft Docs"
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
  - "registros lógicos de replicação de mesclagem [replicação do SQL Server]"
  - "artigos [replicação do SQL Server], registros lógicos"
  - "registros lógicos [replicação do SQL Server]"
ms.assetid: ff847b3a-c6b0-4eaf-b225-2ffc899c5558
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Definir uma rela&#231;&#227;o de registro l&#243;gico entre artigos da tabela de mesclagem
  Este tópico descreve como definir uma relação de registro lógico entre artigos de tabela de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o RMO (Replication Management Objects).  
  
 A replicação de mesclagem permite definir uma relação entre linhas relacionadas em tabelas diferentes. Essas linhas podem então ser processadas como uma unidade transacional durante a sincronização. Um registro lógico pode ser definido entre dois artigos se eles tiverem ou não uma relação de filtro de junção. Para obter mais informações, consulte [grupo alterações nas linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para definir uma relação de registro lógico entre artigos de tabela de mesclagem, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se você adicionar, modificar ou excluir um registro lógico após a inicialização de assinaturas na publicação, será preciso gerar um novo instantâneo e reinicializar todas as assinaturas depois de fazer a alteração. Para obter mais informações sobre os requisitos para alterações de propriedade, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Defina registros lógicos na **Adicionar junção** caixa de diálogo, que está disponível no Assistente de nova publicação e o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
 Os registros lógicos podem ser definidos na caixa de diálogo **Adicionar Junção** apenas se aplicados a um filtro de junção em uma publicação de mesclagem, e se a publicação atender os requisitos para uso de partições pré-calculadas. Para definir os registros lógicos que não se aplicam a filtros de junção e para definir a detecção e resolução de conflitos no nível do registro lógico, é preciso usar procedimentos armazenados.  
  
#### Para definir uma relação de registro lógico.  
  
1.  No **Filtrar linhas da tabela** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione um filtro de linha no **tabelas filtradas** painel.  
  
     Uma relação de registro lógico é associada a um filtro de junção que estende um filtro de linha. Por isso, é preciso definir o filtro de linha antes de poder estender o filtro com uma junção e aplicar uma relação de registro lógico. Após definir o filtro de junção é possível estendê-lo com outro filtro de junção. Para obter mais informações sobre como definir filtros de junção, consulte [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
2.  Clique em **Adicionar**e depois, em **Adicionar Junção para Estender o Filtro Selecionado**.  
  
3.  Defina um filtro de junção na caixa de diálogo **Adicionar Junção** , depois marque a caixa de seleção **Registro Lógico**.  
  
4.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### Para excluir uma relação de registro lógico  
  
-   Exclua apenas a relação de registro lógico ou exclua a relação de registro lógico e o filtro de junção a ela associado.  
  
     Para excluir apenas a relação de registro lógico:  
  
    1.  No **Filtrar linhas** página do Assistente de nova publicação ou o **Filtrar linhas** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione o filtro de junção associado com a relação de registro lógico no **tabelas filtradas** painel e, em seguida, clique **Editar**.  
  
    2.  Na caixa de diálogo **Editar Junção** , desmarque o caixa de seleção **Registro Lógico**.  
  
    3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Para excluir a relação de registro lógico e o filtro de junção a ela associado:  
  
    -   Sobre o **Filtrar linhas** página do Assistente de nova publicação ou **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione um filtro no **tabelas filtradas** painel e, em seguida, clique **Excluir**. Caso o próprio filtro excluído seja estendido por outras junções, essas junções também serão excluídas.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 É possível especificar relações de registro lógico de forma programática entre artigos que usem procedimentos armazenados de replicação.  
  
#### Para definir uma relação de registro lógico sem filtro de junção associado  
  
1.  Se a publicação contiver quaisquer artigos filtrados, execute [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), e observe o valor de **use_partition_groups** no conjunto de resultados.  
  
    -   Se o valor for **1**, partições pré-computadas já estarão sendo usadas.  
  
    -   Se o valor for **0**, em seguida, execute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) no publicador do banco de dados de publicação. Especifique um valor de **use_partition_groups** para **@property** e um valor de **true** para **@value**.  
  
        > [!NOTE]  
        >  Se a publicação não oferecer suporte a partições pré-computadas, os registros lógicos não poderão ser usados. Para obter mais informações, consulte requisitos para usar partições pré-calculadas no tópico [otimizar desempenho de filtro parametrizado com partições pré-calculadas](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md).  
  
    -   Se o valor for NULL, será necessário executar o Snapshot Agent para gerar o instantâneo inicial para a publicação.  
  
2.  Se os artigos que integrarem o registro lógico não existirem, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) no publicador do banco de dados de publicação. Especifique uma das opções de detecção e resolução de conflitos para o registro lógico:  
  
    -   Para detectar e resolver conflitos que ocorrem em linhas relacionadas no registro lógico, especifique um valor de **true** para **@logical_record_level_conflict_detection** e **@logical_record_level_conflict_resolution**.  
  
    -   Para usar a resolução e detecção de conflitos padrão nível de linha ou coluna, especifique um valor de **false** para **@logical_record_level_conflict_detection** e **@logical_record_level_conflict_resolution**, que é o padrão.  
  
3.  Repita a Etapa 2 para cada artigo que integrará o registro lógico. É preciso usar a mesma opção de detecção e resolução de conflitos para cada artigo no registro lógico. Para obter mais informações, consulte [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md).  
  
4.  No publicador do banco de dados de publicação, execute [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md). Especifique **@publication**, o nome de um artigo na relação para **@article**, o nome do segundo artigo para **@join_articlename**, um nome para a relação de **@filtername**, uma cláusula que define a relação entre os dois artigos para **@join_filterclause**, o tipo de associação para **@join_unique_key** e um dos seguintes valores para **@filter_type**:  
  
    -   **2** -define uma relação lógica.  
  
    -   **3** -define uma relação lógica com um filtro de junção.  
  
    > [!NOTE]  
    >  Se um filtro de junção não for usado, a direção da relação entre os dois artigos não será importante.  
  
5.  Repita a Etapa 2 para cada relação de registro lógico remanescente na publicação.  
  
#### Para alterar a detecção e resolução de conflito para registros lógicos  
  
1.  Para detectar e resolver conflitos que ocorrem dentro de linhas relacionadas no registro lógico:  
  
    -   No publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de **logical_record_level_conflict_detection** para **@property** e um valor de **true** para **@value**. Especifique um valor de **1** para **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
    -   No publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de **logical_record_level_conflict_resolution** para **@property** e um valor de **true** para **@value**. Especifique um valor de **1** para **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
2.  Para usar a detecção e resolução de conflitos padrão em nível de linha ou coluna:  
  
    -   No publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de **logical_record_level_conflict_detection** para **@property** e um valor de **false** para **@value**. Especifique um valor de **1** para **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
    -   No publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de **logical_record_level_conflict_resolution** para **@property** e um valor de **false** para **@value**. Especifique um valor de **1** para **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
#### Para remover uma relação de registro lógico.  
  
1.  No Publicador do banco de dados de publicação, execute a consulta a seguir para retornar informações sobre todos as relações de registro lógicos definidos para a publicação especificada:  
  
     [!code-sql[HowTo#sp_ReturnMergeLogicalRecords](../../../relational-databases/replication/codesnippet/tsql/define-a-logical-record-_1.sql)]  
  
     Anote o nome da relação de registro lógico sendo removido da coluna **filtername** no conjunto de resultados.  
  
    > [!NOTE]  
    >  Esta consulta retorna as mesmas informações que [sp_helpmergefilter](../../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md); no entanto, esse sistema de procedimento armazenado somente retorna informações sobre relações de registro lógico são também filtros de junção.  
  
2.  No publicador do banco de dados de publicação, execute [sp_dropmergefilter](../../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md). Especifique **@publication**, o nome de um dos artigos da relação para **@article**, e o nome da relação da Etapa 1 para **@filtername**.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Esse exemplo habilita partições pré-computadas em uma publicação existente e cria um registro lógico que inclui os dois novos artigos para as tabelas `SalesOrderHeader` e `SalesOrderDetail` .  
  
 [!code-sql[HowTo#sp_AddMergeLogicalRecord](../../../relational-databases/replication/codesnippet/tsql/define-a-logical-record-_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
  
> [!NOTE]  
>  A replicação de mesclagem lhe permite também especificar que os conflitos sejam rastreados e resolvidos em nível de registro lógico, mas essas opções não podem ser definidas usando-se RMO.  
  
#### Para definir uma relação de registro lógico sem filtro de junção associado  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePublication> classe, defina o <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a conexão criada na etapa 1.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Se o <xref:Microsoft.SqlServer.Replication.MergePublication.PartitionGroupsOption%2A> está definida como <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.False>, defina-o como <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.True>.  
  
5.  Se os artigos que farão parte do registro lógico não existir, crie uma instância do <xref:Microsoft.SqlServer.Replication.MergeArticle> de classe e defina as seguintes propriedades:  
  
    -   O nome do artigo para <xref:Microsoft.SqlServer.Replication.Article.Name%2A>.  
  
    -   O nome da publicação para <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>.  
  
    -   (Opcional) Se o artigo é filtrado horizontalmente, especifique a cláusula de filtro de linha para o <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> propriedade. Use essa propriedade para especificar um filtro de linha estático ou com parâmetros. Para obter mais informações, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
     Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  Chamar o <xref:Microsoft.SqlServer.Replication.Article.Create%2A> método.  
  
7.  Repita a etapa 5 e 6 para cada artigo que integra o registro lógico.  
  
8.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> classe para definir a relação de registro lógico entre artigos. Em seguida, defina as seguintes propriedades:  
  
    -   O nome do artigo filho na relação de registro lógico para o <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.ArticleName%2A> propriedade.  
  
    -   O nome do artigo pai existente na relação de registro lógico para o <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinArticleName%2A> propriedade.  
  
    -   Um nome para a relação de registro lógico para o <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterName%2A> propriedade.  
  
    -   A expressão que define a relação para o <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinFilterClause%2A> propriedade.  
  
    -   Um valor de <xref:Microsoft.SqlServer.Replication.FilterTypes.LogicalRecordLink> para o <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterTypes%2A> propriedade. Se a relação de registro lógico também é um filtro de junção, especifique um valor de <xref:Microsoft.SqlServer.Replication.FilterTypes.JoinFilterAndLogicalRecordLink> para essa propriedade. Para obter mais informações, consulte [grupo alterações nas linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
9. Chamar o <xref:Microsoft.SqlServer.Replication.MergeArticle.AddMergeJoinFilter%2A> método no objeto que representa o artigo filho na relação. Passar o <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> objeto da etapa 8 para definir a relação.  
  
10. Repita as etapas 8 e 9 para cada relação de registro lógico remanescente na publicação.  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Esse exemplo cria um registro lógico que inclui os dois novos artigos para as tabelas `SalesOrderHeader` e `SalesOrderDetail` .  
  
 [!code-csharp[HowTo#rmo_CreateLogicalRecord](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createlogicalrecord)]  
  
 [!code-vb[HowTo#rmo_vb_CreateLogicalRecord](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createlogicalrecord)]  
  
## Consulte também  
 [Definir e modificar um filtro de junção entre artigos de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [Agrupar alterações a linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [Otimizar o desempenho de filtro parametrizado com partições pré-computadas](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)   
 [Agrupar alterações a linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)  
  
  