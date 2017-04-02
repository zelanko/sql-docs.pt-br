---
title: "Excluir uma publica&#231;&#227;o | Microsoft Docs"
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
  - "removendo publicações"
  - "publicações [replicação do SQL Server], excluindo"
  - "artigos [replicação do SQL Server], excluindo"
  - "excluindo publicações"
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Excluir uma publica&#231;&#227;o
  Este tópico descreve como excluir uma publicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para excluir uma publicação, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exclua publicações da pasta **Publicações Locais** no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
#### Para excluir uma publicação  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com botão direito a publicação que você deseja excluir e, em seguida, clique em **Excluir**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As publicações podem ser excluídas programaticamente usando procedimentos armazenados de replicação. Os procedimentos armazenados que você usar dependerão do tipo de publicação a ser excluída.  
  
> [!NOTE]  
>  Excluir uma publicação não remove objetos publicados do banco de dados de publicação ou objetos correspondentes do banco de dados de assinatura. Use o comando `DROP <object>` para remover esses objetos manualmente, se necessário.  
  
#### Para excluir uma publicação de instantâneo ou transacional  
  
1.  Siga um destes procedimentos:  
  
    -   Para excluir uma única publicação, execute [sp_droppublication](../../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md) no publicador do banco de dados de publicação.  
  
    -   Para excluir todas as publicações em e remover todos os objetos de replicação de um banco de dados publicado, execute [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) no Editor. Especifique um valor de **tran** para **@type**. (Opcional) Se o distribuidor não pode ser acessado ou se o status do banco de dados é suspeito ou offline, especifique um valor de **1** para **@force**. (Opcional) Especifique o nome do banco de dados **@dbname** se [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) não é executado no banco de dados de publicação.  
  
        > [!NOTE]  
        >  Especificando um valor de **1** para **@force** pode deixar objetos de publicação relacionadas à replicação no banco de dados.  
  
2.  (Opcional) Se esse banco de dados não tem outras publicações, execute [sp_replicationdboption & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) Para desabilitar publicação do banco de dados atual usando replicação de instantâneo ou transacional.  
  
3.  (Opcional) No assinante no banco de dados de assinatura, execute [sp_subscription_cleanup](../../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) para remover quaisquer metadados de replicação remanescentes no banco de dados de assinatura.  
  
#### Para excluir uma publicação de mesclagem  
  
1.  Siga um destes procedimentos:  
  
    -   Para excluir uma única publicação, execute [sp_dropmergepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md) o publicador do banco de dados de publicação.  
  
    -   Para excluir todas as publicações em e remover todos os objetos de replicação de um banco de dados publicado, execute [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) no Editor. Especifique um valor de **merge** para **@type**. (Opcional) Se o distribuidor não pode ser acessado ou se o status do banco de dados é suspeito ou offline, especifique um valor de **1** para **@force**. (Opcional) Especifique o nome do banco de dados **@dbname** se [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) não é executado no banco de dados de publicação.  
  
        > [!NOTE]  
        >  Especificando um valor de **1** para **@force** pode deixar objetos de publicação relacionadas à replicação no banco de dados.  
  
2.  (Opcional) Se esse banco de dados não tem outras publicações, execute [sp_replicationdboption & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) Para desabilitar publicação do banco de dados atual usando replicação de mesclagem.  
  
3.  (Opcional) No assinante no banco de dados de assinatura, execute [sp_mergesubscription_cleanup & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md) Para remover quaisquer metadados de replicação remanescentes no banco de dados de assinatura.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Este exemplo mostra como remover uma publicação transacional e desabilitar publicação transacional para um banco de dados. Este exemplo pressupõe que todas as assinaturas foram previamente removidas. Para obter mais informações, consulte [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) ou [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md).  
  
 [!code-sql[HowTo#sp_droppublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_1.sql)]  
  
 Este exemplo mostra como remover uma publicação de mesclagem e desabilitar publicação de mesclagem para um banco de dados. Este exemplo pressupõe que todas as assinaturas foram previamente removidas. Para obter mais informações, consulte [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) ou [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md).  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 É possível excluir publicações de forma programada usando o RMO (Replication Management Objects). As classes de RMO usadas para remover uma publicação dependem do tipo de publicação a ser removida.  
  
#### Para remover uma publicação transacional ou instantâneo  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPublication> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a conexão criada na etapa 1.  
  
4.  Verifique o <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> propriedade para verificar se a publicação existe. Se o valor dessa propriedade for **false**, as propriedades de publicação na etapa 3 foram definidas incorretamente ou a publicação não existe.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> método.  
  
6.  (Opcional) Se nenhuma outra publicação transacional existir para esse banco de dados, ele pode ser desabilitado para a publicação transacional, como se segue:  
  
    1.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> classe. Definir o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a instância do <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
    2.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se esse método retorna **false**, confirme que o banco de dados existe.  
  
    3.  Definir o <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> propriedade **false**.  
  
    4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método.  
  
7.  Feche as conexões.  
  
#### Para remover uma publicação de mesclagem  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePublication> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propriedades para a publicação e defina o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a conexão criada na etapa 1.  
  
4.  Verifique o <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> propriedade para verificar se a publicação existe. Se o valor dessa propriedade for **false**, as propriedades de publicação na etapa 3 foram definidas incorretamente ou a publicação não existe.  
  
5.  Chamar o <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> método.  
  
6.  (Opcional) Se nenhuma outra publicação de mesclagem existir para esse banco de dados, ele pode ser desabilitado para a publicação de mesclagem, como se segue:  
  
    1.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> classe. Definir o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade para a instância do <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
    2.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se esse método retornar **false**, verifique se o banco de dados existe.  
  
    3.  Definir o <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> propriedade **false**.  
  
    4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método.  
  
7.  Feche as conexões.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 O exemplo a seguir exclui uma publicação transacional. Se nenhuma outra publicação transacional existir para esse banco de dados, a publicação transacional será também desabilitada.  
  
 [!code-csharp[HowTo#rmo_DropTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 O exemplo a seguir exclui uma publicação de mesclagem. Se nenhuma outra publicação de mesclagem existir para esse banco de dados, a publicação de mesclagem será também desabilitada.  
  
 [!code-csharp[HowTo#rmo_DropMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## Consulte também  
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  