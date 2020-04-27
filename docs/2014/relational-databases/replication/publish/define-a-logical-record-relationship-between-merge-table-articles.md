---
title: Definir uma relação de registro lógico entre artigos de tabela de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ff847b3a-c6b0-4eaf-b225-2ffc899c5558
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c1c5be804f60fa57b677a418c19d8aadee23f22
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62691667"
---
# <a name="define-a-logical-record-relationship-between-merge-table-articles"></a>Definir uma relação de registro lógico entre artigos da tabela de mesclagem
  Este tópico descreve como definir uma relação de registro lógico entre artigos de tabela de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o RMO (Replication Management Objects).  
  
 A replicação de mesclagem permite definir uma relação entre linhas relacionadas em tabelas diferentes. Essas linhas podem então ser processadas como uma unidade transacional durante a sincronização. Um registro lógico pode ser definido entre dois artigos se eles tiverem ou não uma relação de filtro de junção. Para obter mais informações, consulte [Agrupar alterações a linhas relacionadas com registros lógicos](../merge/group-changes-to-related-rows-with-logical-records.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para definir uma relação de registro lógico entre artigos de tabela de mesclagem, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Se você adicionar, modificar ou excluir um registro lógico após a inicialização de assinaturas na publicação, será preciso gerar um novo instantâneo e reinicializar todas as assinaturas depois de fazer a alteração. Para obter mais informações sobre os requisitos para alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Defina registros lógicos na caixa de diálogo **Adicionar Junção**, disponível no Assistente para Nova Publicação e na caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](create-a-publication.md) e [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md).  
  
 Os registros lógicos podem ser definidos na caixa de diálogo **Adicionar Junção** apenas se aplicados a um filtro de junção em uma publicação de mesclagem, e se a publicação atender os requisitos para uso de partições pré-calculadas. Para definir os registros lógicos que não se aplicam a filtros de junção e para definir a detecção e resolução de conflitos no nível do registro lógico, é preciso usar procedimentos armazenados.  
  
#### <a name="to-define-a-logical-record-relationship"></a>Para definir uma relação de registro lógico.  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, selecione um filtro no painel **Tabelas Filtradas**.  
  
     Uma relação de registro lógico é associada a um filtro de junção que estende um filtro de linha. Por isso, é preciso definir o filtro de linha antes de poder estender o filtro com uma junção e aplicar uma relação de registro lógico. Após definir o filtro de junção é possível estendê-lo com outro filtro de junção. Para obter mais informações sobre como definir filtros de junção, consulte [Definir e modificar um filtro de junção entre artigos de mesclagem](define-and-modify-a-join-filter-between-merge-articles.md).  
  
2.  Clique em **Adicionar**e depois, em **Adicionar Junção para Estender o Filtro Selecionado**.  
  
3.  Defina um filtro de junção na caixa de diálogo **Adicionar Junção** , depois marque a caixa de seleção **Registro Lógico**.  
  
4.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### <a name="to-delete-a-logical-record-relationship"></a>Para excluir uma relação de registro lógico  
  
-   Exclua apenas a relação de registro lógico ou exclua a relação de registro lógico e o filtro de junção a ela associado.  
  
     Para excluir apenas a relação de registro lógico:  
  
    1.  Na página **Filtrar Linhas** do Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, selecione o filtro de junção associado à relação de registo lógico no painel **Tabelas Filtradas** e clique em **Editar**.  
  
    2.  Na caixa de diálogo **Editar Junção** , desmarque o caixa de seleção **Registro Lógico**.  
  
    3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Para excluir a relação de registro lógico e o filtro de junção a ela associado:  
  
    -   Na página **Filtrar Linhas** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades da Publicação – \<Publicação>**, selecione um filtro no painel **Tabelas Filtradas** e, em seguida, clique em **Excluir**. Caso o próprio filtro excluído seja estendido por outras junções, essas junções também serão excluídas.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 É possível especificar relações de registro lógico de forma programática entre artigos que usem procedimentos armazenados de replicação.  
  
#### <a name="to-define-a-logical-record-relationship-without-an-associated-join-filter"></a>Para definir uma relação de registro lógico sem filtro de junção associado  
  
1.  Se a publicação contiver quaisquer artigos filtrados, execute [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), e observe o valor de **use_partition_groups** no conjunto de resultados.  
  
    -   Se o valor for **1**, partições pré-computadas já estarão sendo usadas.  
  
    -   Se o valor for **0**, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) ao Publicador do banco de dados de publicação. Especifique um valor de **use_partition_groups** para **@property** e um valor de **true** para **@value**.  
  
        > [!NOTE]  
        >  Se a publicação não oferecer suporte a partições pré-computadas, os registros lógicos não poderão ser usados. Para obter mais informações, consulte Requisitos para usar partições pré-computadas no tópico [Otimizar o desempenho de filtro parametrizado com partições pré-computadas](../merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
    -   Se o valor for NULL, será necessário executar o Snapshot Agent para gerar o instantâneo inicial para a publicação.  
  
2.  Se os artigos que integrarem o registro lógico não existirem, execute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) no Publicador do banco de dados de publicação. Especifique uma das opções de detecção e resolução de conflitos para o registro lógico:  
  
    -   Para detectar e resolver conflitos que ocorrem dentro das linhas relacionadas no registro lógico, especifique um valor de **true** para **@logical_record_level_conflict_detection** e **@logical_record_level_conflict_resolution**.  
  
    -   Para usar a detecção e resolução de conflitos padrão em nível de linha ou coluna, especifique um valor `false` de **@logical_record_level_conflict_detection** para **@logical_record_level_conflict_resolution**e, que é o padrão.  
  
3.  Repita a Etapa 2 para cada artigo que integrará o registro lógico. É preciso usar a mesma opção de detecção e resolução de conflitos para cada artigo no registro lógico. Para obter mais informações, consulte [Detectando e resolvendo conflitos em registros lógicos](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
4.  No Publicador do banco de dados de publicação, execute [sp_addmergefilter](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql). Especifique **@publication** **@article**, o nome de um artigo na relação para, o nome do segundo artigo para **@join_articlename**, um nome para a relação para **@filtername**, uma cláusula que define a relação entre os dois artigos para **@join_filterclause**, o tipo de junção para **@join_unique_key** e um dos seguintes valores para: **@filter_type**  
  
    -   **2** - Define uma relação lógica.  
  
    -   **3** - Define uma relação lógica com um filtro de junção.  
  
    > [!NOTE]  
    >  Se um filtro de junção não for usado, a direção da relação entre os dois artigos não será importante.  
  
5.  Repita a Etapa 2 para cada relação de registro lógico remanescente na publicação.  
  
#### <a name="to-change-conflict-detection-and-resolution-for-logical-records"></a>Para alterar a detecção e resolução de conflito para registros lógicos  
  
1.  Para detectar e resolver conflitos que ocorrem dentro de linhas relacionadas no registro lógico:  
  
    -   No Publicador do banco de dados de publicação, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique um valor de **logical_record_level_conflict_detection** para **@property** e um valor de **true** para **@value**. Especifique um valor de **1** para **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
    -   No Publicador do banco de dados de publicação, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique um valor de **logical_record_level_conflict_resolution** para **@property** e um valor de **true** para **@value**. Especifique um valor de **1** para **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
2.  Para usar a detecção e resolução de conflitos padrão em nível de linha ou coluna:  
  
    -   No Publicador do banco de dados de publicação, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique um valor de **logical_record_level_conflict_detection** para **@property** e um valor de `false` para **@value**. Especifique um valor de **1** para **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
    -   No Publicador do banco de dados de publicação, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique um valor de **logical_record_level_conflict_resolution** para **@property** e um valor de `false` para **@value**. Especifique um valor de **1** para **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
#### <a name="to-remove-a-logical-record-relationship"></a>Para remover uma relação de registro lógico.  
  
1.  No Publicador do banco de dados de publicação, execute a consulta a seguir para retornar informações sobre todos as relações de registro lógicos definidos para a publicação especificada:  
  
     [!code-sql[HowTo#sp_ReturnMergeLogicalRecords](../../../snippets/tsql/SQL15/replication/howto/tsql/createlogicalrecordpub.sql#sp_returnmergelogicalrecords)]  
  
     Anote o nome da relação de registro lógico sendo removido da coluna `filtername` no conjunto de resultados.  
  
    > [!NOTE]  
    >  Essa consulta retorna as mesmas informações de [sp_helpmergefilter](/sql/relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql); no entanto, esse procedimento armazenado de sistema retorna apenas informações sobre relações de registro lógico que são também filtros de junção.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_dropmergefilter](/sql/relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql). Especifique **@publication**, o nome de um dos artigos na relação para **@article**e o nome da relação da etapa 1 para. **@filtername**  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a>Exemplo (Transact-SQL)  
 Esse exemplo habilita partições pré-computadas em uma publicação existente e cria um registro lógico que inclui os dois novos artigos para as tabelas `SalesOrderHeader` e `SalesOrderDetail` .  
  
 [!code-sql[HowTo#sp_AddMergeLogicalRecord](../../../snippets/tsql/SQL15/replication/howto/tsql/createlogicalrecordpub.sql#sp_addmergelogicalrecord)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
  
> [!NOTE]  
>  A replicação de mesclagem lhe permite também especificar que os conflitos sejam rastreados e resolvidos em nível de registro lógico, mas essas opções não podem ser definidas usando-se RMO.  
  
#### <a name="to-define-a-logical-record-relationship-without-an-associated-join-filter"></a>Para definir uma relação de registro lógico sem filtro de junção associado  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> , defina <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e propriedades <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação, e defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada no etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar `false`, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Se a propriedade <xref:Microsoft.SqlServer.Replication.MergePublication.PartitionGroupsOption%2A> for definida como <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.False>,  defina-a para <xref:Microsoft.SqlServer.Replication.PartitionGroupsOption.True>.  
  
5.  Se os artigos que farão parte do registro lógico não existem, crie uma instância de classe <xref:Microsoft.SqlServer.Replication.MergeArticle> e defina as seguintes propriedades:  
  
    -   Nome do artigo para <xref:Microsoft.SqlServer.Replication.Article.Name%2A>.  
  
    -   Nome da publicação para <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>.  
  
    -   (Opcional) Se o artigo for filtrado horizontalmente, especifique a cláusula do filtro da linha para a propriedade <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> . Use essa propriedade para especificar um filtro de linha estático ou com parâmetros. Para obter mais informações, consulte [Filtros de linha com parâmetros](../merge/parameterized-filters-parameterized-row-filters.md).  
  
     Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.Article.Create%2A> .  
  
7.  Repita a etapa 5 e 6 para cada artigo que integra o registro lógico.  
  
8.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> para definir a relação de registro lógica entre artigos. Em seguida, defina as seguintes propriedades:  
  
    -   O nome do artigo filho na relação de registro lógico para a propriedade <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.ArticleName%2A> .  
  
    -   O nome do artigo pai existente na relação de registro lógico para a propriedade <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinArticleName%2A> .  
  
    -   Um nome para a relação de registro lógico para a propriedade <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterName%2A> .  
  
    -   A expressão que define a relação para a propriedade <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.JoinFilterClause%2A> .  
  
    -   O valor de <xref:Microsoft.SqlServer.Replication.FilterTypes.LogicalRecordLink> para a propriedade <xref:Microsoft.SqlServer.Replication.MergeJoinFilter.FilterTypes%2A> . Se a relação de registro lógica também for um filtro de junção, especifique um valor de <xref:Microsoft.SqlServer.Replication.FilterTypes.JoinFilterAndLogicalRecordLink> para essa propriedade. Para obter mais informações, consulte [Agrupar alterações a linhas relacionadas com registros lógicos](../merge/group-changes-to-related-rows-with-logical-records.md).  
  
9. Chame o método <xref:Microsoft.SqlServer.Replication.MergeArticle.AddMergeJoinFilter%2A> no objeto que representa o artigo filho na relação. Passe o objeto <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> da etapa 8 para definir a relação.  
  
10. Repita as etapas 8 e 9 para cada relação de registro lógico remanescente na publicação.  
  
###  <a name="example-rmo"></a><a name="PShellExample"></a>Exemplo (RMO)  
 Esse exemplo cria um registro lógico que inclui os dois novos artigos para as tabelas `SalesOrderHeader` e `SalesOrderDetail` .  
  
 [!code-csharp[HowTo#rmo_CreateLogicalRecord](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createlogicalrecord)]  
  
 [!code-vb[HowTo#rmo_vb_CreateLogicalRecord](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createlogicalrecord)]  
  
## <a name="see-also"></a>Consulte Também  
 [Definir e modificar um filtro de junção entre artigos de mesclagem](define-and-modify-a-join-filter-between-merge-articles.md)   
 [Definir e modificar um filtro de linha parametrizado para um artigo de mesclagem](define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Definir e modificar um filtro de linha estático](define-and-modify-a-static-row-filter.md)   
 [Agrupar alterações em linhas relacionadas com registros lógicos](../merge/group-changes-to-related-rows-with-logical-records.md)   
 [Otimizar o desempenho de filtro com parâmetros com partições de computação](../merge/parameterized-filters-optimize-for-precomputed-partitions.md)   
 [Agrupar alterações em linhas relacionadas com registros lógicos](../merge/group-changes-to-related-rows-with-logical-records.md)  
  
  
