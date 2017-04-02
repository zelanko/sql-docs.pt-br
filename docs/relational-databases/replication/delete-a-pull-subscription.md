---
title: "Excluir uma assinatura pull | Microsoft Docs"
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
  - "removendo assinaturas"
  - "excluindo assinaturas"
  - "assinaturas pull [replicação do SQL Server], excluindo"
  - "assinaturas [replicação do SQL Server], pull"
ms.assetid: 997c0b8e-d8d9-4eed-85b1-6baa1f8594ce
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Excluir uma assinatura pull
  Este tópico descreve como excluir uma assinatura pull no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para excluir uma assinatura pull, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Excluir uma assinatura pull no publicador (da **publicações locais** pasta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) ou no assinante (da **assinaturas locais** pasta). A exclusão de uma assinatura não remove objetos ou dados da assinatura; eles devem ser removidos manualmente.  
  
#### Para excluir uma assinatura pull no Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação associada à assinatura que você deseja excluir.  
  
4.  Clique com botão direito a assinatura e, em seguida, clique em **Excluir**.  
  
5.  Na caixa de diálogo de confirmação, selecione onde conectar-se ao Assinante para excluir as informações de assinatura. Se você desmarcar a caixa de seleção **Conectar ao Assinante** , você deve conectar-se ao Assinante depois para excluir as informações.  
  
#### Para excluir uma assinatura pull no Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com botão direito a assinatura que você deseja excluir e, em seguida, clique em **Excluir**.  
  
4.  Na caixa de diálogo de confirmação, selecione se deseja se conectar ao Publicador para excluir as informações de assinatura. Se você desmarcar a caixa de seleção **Conectar-se ao Publicador** , será necessário se conectar ao Publicador posteriormente para excluir as informações.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As assinaturas pull podem ser excluídas programaticamente, por meio de procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### Para excluir uma assinatura pull em uma publicação de instantâneo ou transacional  
  
1.  No assinante no banco de dados de assinatura, execute [sp_droppullsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md). Especifique **@publication**, **@publisher**, e **@publisher_db**.  
  
2.  No publicador do banco de dados de publicação, execute [sp_dropsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). Especifique **@publication** e **@subscriber**. Especifique um valor de **all** para **@article**. (Opcional) Se o distribuidor não puder ser acessado, especifique um valor de **1** para **@ignore_distributor** para excluir a assinatura sem remover objetos relacionados no distribuidor.  
  
#### Para excluir uma assinatura pull em uma publicação de mesclagem.  
  
1.  No assinante no banco de dados de assinatura, execute [sp_dropmergepullsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md). Especifique **@publication**, **@publisher**, e **@publisher_db**.  
  
2.  No publicador do banco de dados de publicação, execute [sp_dropmergesubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, e **@subscriber_db**. Especifique um valor de **recepção** para **@subscription_type**. (Opcional) Se o distribuidor não puder ser acessado, especifique um valor de **1** para **@ignore_distributor** para excluir a assinatura sem remover objetos relacionados no distribuidor.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 O exemplo a seguir exclui uma nova assinatura pull para uma publicação transacional. O primeiro lote é executado no Assinante e o segundo no Publicador.  
  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_1.sql)]  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_2.sql)]  
  
 O exemplo a seguir exclui uma assinatura pull em uma publicação de mesclagem. O primeiro lote é executado no Assinante e o segundo no Publicador.  
  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_3.sql)]  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_4.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Você pode criar assinaturas pull programaticamente, usando o RMO (Replication Management Objects). As classes RMO que você usa para excluir uma assinatura pull dependem do tipo de publicação para a qual a assinatura pull é inscrita.  
  
#### Para excluir uma assinatura pull em uma publicação de instantâneo ou transacional  
  
1.  Criar conexões com o assinante e o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPullSubscription> de classe e defina o <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propriedades. Use a conexão de assinante da etapa 1 para definir o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
3.  Verifique o <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> propriedade para verificar a existência de assinatura. Se o valor dessa propriedade for **false**, as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura não existe.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> método.  
  
5.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPublication> classe usando a conexão do publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
6.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se esse método retornar **false**, as propriedades especificadas na etapa 5 estão incorretas ou a publicação não existe no servidor.  
  
7.  Chamar o <xref:Microsoft.SqlServer.Replication.TransPublication.RemovePullSubscription%2A> método. Especifique o nome do Assinante e o banco de dados de assinatura para o *subscriber* e parâmetros *subscriberDB* .  
  
#### Para excluir uma assinatura pull em uma publicação de mesclagem.  
  
1.  Criar conexões com o assinante e o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePullSubscription> de classe e defina o <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propriedades. Use a conexão da etapa 1 para definir o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
3.  Verifique o <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> propriedade para verificar a existência de assinatura. Se o valor dessa propriedade for **false**, as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura não existe.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> método.  
  
5.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePublication> classe usando a conexão do publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
6.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Se esse método retornar **false**, as propriedades especificadas na etapa 5 estão incorretas ou a publicação não existe no servidor.  
  
7.  Chamar o <xref:Microsoft.SqlServer.Replication.MergePublication.RemovePullSubscription%2A> método. Especifique o nome do Assinante e o banco de dados de assinatura para o *subscriber* e parâmetros *subscriberDB* .  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo exclui uma assinatura pull a uma publicação transacional e remove o registro de assinatura no Publicador.  
  
 [!code-csharp[HowTo#rmo_DropTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpullsub)]  
  
 Esse exemplo exclui uma assinatura pull para uma publicação de mesclagem e remove o registro de assinatura no Publicador.  
  
 [!code-csharp[HowTo#rmo_DropMergePullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepullsub)]  
  
## Consulte também  
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  