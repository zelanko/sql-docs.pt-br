---
title: Excluir uma assinatura push | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing subscriptions
- push subscriptions [SQL Server replication], deleting
- deleting subscriptions
- subscriptions [SQL Server replication], push
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 7fac24aec092ef65bb390d8df020999647f215c6
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72908265"
---
# <a name="delete-a-push-subscription"></a>Excluir uma assinatura push
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como excluir uma assinatura push no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para excluir uma assinatura push, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exclua uma assinatura push no Publicador (da pasta **Publicações Locais** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) ou no Assinante (da pasta **Assinaturas Locais** ). A exclusão de uma assinatura não remove objetos ou dados da assinatura; eles devem ser removidos manualmente.  
  
#### <a name="to-delete-a-push-subscription-at-the-publisher"></a>Para excluir uma assinatura push no Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação associada à assinatura que você deseja excluir.  
  
4.  Clique como botão direito do mouse na assinatura e, então, clique em **Excluir**.  
  
5.  Na caixa de diálogo de confirmação, selecione onde conectar-se ao Assinante para excluir as informações de assinatura. Se você desmarcar a caixa de seleção **Conectar-se ao Assinante** , será necessário conectar-se ao Assinante, posteriormente, para excluir as informações.  

#### <a name="to-delete-a-push-subscription-at-the-subscriber"></a>Para excluir uma assinatura push no Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito na assinatura a ser excluída e clique em **Excluir**.  
  
4.  Na caixa de diálogo de confirmação, selecione se deseja se conectar ao Publicador para excluir as informações de assinatura. Se você desmarcar a caixa de seleção **Conectar-se ao Publicador** , será necessário se conectar ao Publicador posteriormente para excluir as informações.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As assinaturas push podem ser excluídas programaticamente, usando procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para excluir uma assinatura push de um instantâneo ou publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). Especifique **\@publication** e **\@subscriber**. Especifique um valor igual a **all** em **\@article**. (Opcional) Se o Distribuidor não puder ser acessado, especifique um valor igual a **1** em **\@ignore_distributor** para excluir a assinatura sem remover objetos relacionados no Distribuidor.  
  
2.  No Assinante no banco de dados de assinatura, execute [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) para remover metadados de replicação no banco de dados de assinatura.  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>Para excluir uma assinatura push para uma publicação de mesclagem.  
  
1.  No Publicador, execute [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md) especificando **\@publication**, **\@subscriber** e **\@subscriber_db**. (Opcional) Se o Distribuidor não puder ser acessado, especifique um valor igual a **1** em **\@ignore_distributor** para excluir a assinatura sem remover objetos relacionados no Distribuidor.  
  
2.  No Assinante no banco de dados de assinatura, execute [sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md). Especifique **\@publisher**, **\@publisher_db** e **\@publication**. Isso remove metadados de mesclagem do banco de dados de assinatura.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo exclui uma assinatura push para uma publicação transacional.  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_1.sql)]  
  
 Esse exemplo exclui uma assinatura push para uma publicação de mesclagem.  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 As classes RMO a serem usadas para excluir uma assinatura push dependem do tipo de publicação em que a assinatura push está inscrita.  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para excluir uma assinatura push de um instantâneo ou publicação transacional  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.TransSubscription>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>e <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> .  
  
4.  Defina a propriedade <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para verificar se a assinatura existe. Se o valor dessa propriedade for **false**, as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura não existe.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> .  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>Para excluir uma assinatura push para uma publicação de mesclagem.  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeSubscription>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>e <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> .  
  
4.  Defina a propriedade <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para verificar se a assinatura existe. Se o valor dessa propriedade for **false**, as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura não existe.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> .  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Você pode excluir assinaturas push programaticamente, usando o RMO (Replication Management Objects).  
  
 [!code-cs[HowTo#rmo_DropTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## <a name="see-also"></a>Consulte Também  
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
