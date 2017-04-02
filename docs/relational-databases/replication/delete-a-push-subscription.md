---
title: "Excluir uma assinatura push | Microsoft Docs"
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
  - "removing subscriptions"
  - "push subscriptions [SQL Server replication], deleting"
  - "deleting subscriptions"
  - "assinaturas [replicação do SQL Server], push"
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Excluir uma assinatura push
  Este tópico descreve como excluir uma assinatura push no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para excluir uma assinatura push, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Excluir uma assinatura push no publicador (da **publicações locais** pasta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) ou no assinante (da **assinaturas locais** pasta). A exclusão de uma assinatura não remove objetos ou dados da assinatura; eles devem ser removidos manualmente.  
  
#### Para excluir uma assinatura push no Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação associada à assinatura que você deseja excluir.  
  
4.  Clique com botão direito a assinatura e, em seguida, clique em **Excluir**.  
  
5.  Na caixa de diálogo de confirmação, selecione onde conectar-se ao Assinante para excluir as informações de assinatura. Se você desmarcar a caixa de seleção **Conectar-se ao Assinante** , será necessário conectar-se ao Assinante, posteriormente, para excluir as informações.  
  
#### Para excluir uma assinatura push no Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com botão direito a assinatura que você deseja excluir e, em seguida, clique em **Excluir**.  
  
4.  Na caixa de diálogo de confirmação, selecione se deseja se conectar ao Publicador para excluir as informações de assinatura. Se você desmarcar a caixa de seleção **Conectar-se ao Publicador** , será necessário se conectar ao Publicador posteriormente para excluir as informações.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As assinaturas push podem ser excluídas programaticamente, usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### Para excluir uma assinatura push de um instantâneo ou publicação transacional  
  
1.  No publicador do banco de dados de publicação, execute [sp_dropsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). Especifique **@publication** e **@subscriber**. Especifique um valor de **all** para **@article**. (Opcional) Se o distribuidor não puder ser acessado, especifique um valor de **1** para **@ignore_distributor** para excluir a assinatura sem remover objetos relacionados no distribuidor.  
  
2.  No assinante no banco de dados de assinatura, execute [sp_subscription_cleanup & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) Para remover os metadados de replicação no banco de dados de assinatura.  
  
#### Para excluir uma assinatura push para uma publicação de mesclagem.  
  
1.  No publicador, execute [sp_dropmergesubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md), especificando **@publication**, **@subscriber** e **@subscriber_db**. (Opcional) Se o distribuidor não puder ser acessado, especifique um valor de **1** para **@ignore_distributor** para excluir a assinatura sem remover objetos relacionados no distribuidor.  
  
2.  No assinante no banco de dados de assinatura, execute [sp_mergesubscription_cleanup & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md). Especifique **@publisher**, **@publisher_db**, e **@publication**. Isso remove metadados de mesclagem do banco de dados de assinatura.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo exclui uma assinatura push para uma publicação transacional.  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_1.sql)]  
  
 Esse exemplo exclui uma assinatura push para uma publicação de mesclagem.  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 As classes RMO a serem usadas para excluir uma assinatura push dependem do tipo de publicação em que a assinatura push está inscrita.  
  
#### Para excluir uma assinatura push de um instantâneo ou publicação transacional  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransSubscription> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, e <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> Propriedades.  
  
4.  Definir o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
5.  Verifique o <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> propriedade para verificar a existência de assinatura. Se o valor dessa propriedade for **false**, as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura não existe.  
  
6.  Chamar o <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> método.  
  
#### Para excluir uma assinatura push para uma publicação de mesclagem.  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeSubscription> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, e <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> Propriedades.  
  
4.  Definir o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
5.  Verifique o <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> propriedade para verificar a existência de assinatura. Se o valor dessa propriedade for **false**, as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura não existe.  
  
6.  Chamar o <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> método.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Você pode excluir assinaturas push programaticamente, usando o RMO (Replication Management Objects).  
  
 [!code-csharp[HowTo#rmo_DropTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## Consulte também  
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  