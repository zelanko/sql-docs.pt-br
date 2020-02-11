---
title: Excluir uma assinatura pull | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing subscriptions
- deleting subscriptions
- pull subscriptions [SQL Server replication], deleting
- subscriptions [SQL Server replication], pull
ms.assetid: 997c0b8e-d8d9-4eed-85b1-6baa1f8594ce
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ac5d4f7d199e3ee3de6ffb43e2c43e232681b0d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721463"
---
# <a name="delete-a-pull-subscription"></a>Excluir uma assinatura pull
  Este tópico descreve como excluir uma assinatura pull no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para excluir uma assinatura pull, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exclua uma assinatura pull no Publicador (da pasta **Publicações Locais** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) ou no Assinante (da pasta **Assinaturas Locais** ). A exclusão de uma assinatura não remove objetos ou dados da assinatura; eles devem ser removidos manualmente.  
  
#### <a name="to-delete-a-pull-subscription-at-the-publisher"></a>Para excluir uma assinatura pull no Publicador  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação associada à assinatura que você deseja excluir.  
  
4.  Clique como botão direito do mouse na assinatura e, então, clique em **Excluir**.  
  
5.  Na caixa de diálogo de confirmação, selecione onde conectar-se ao Assinante para excluir as informações de assinatura. Se você desmarcar a caixa de seleção **Conectar ao Assinante** , você deve conectar-se ao Assinante depois para excluir as informações.  
  
#### <a name="to-delete-a-pull-subscription-at-the-subscriber"></a>Para excluir uma assinatura pull no Assinante  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito na assinatura a ser excluída e clique em **Excluir**.  
  
4.  Na caixa de diálogo de confirmação, selecione se deseja se conectar ao Publicador para excluir as informações de assinatura. Se você desmarcar a caixa de seleção **Conectar-se ao Publicador** , será necessário se conectar ao Publicador posteriormente para excluir as informações.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As assinaturas pull podem ser excluídas programaticamente, por meio de procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### <a name="to-delete-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para excluir uma assinatura pull em uma publicação de instantâneo ou transacional  
  
1.  No Assinante no banco de dados de assinatura, execute [sp_droppullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql). Especifique **@publication**, **@publisher**, e **@publisher_db**.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql). Especifique **@publication** e **@subscriber**. Especifique um valor de **all** para **@article**. (Opcional) Se o Distribuidor não puder ser acessado, especifique um valor de **1** para **@ignore_distributor** para excluir a assinatura sem remover objetos relacionados no Distribuidor.  
  
#### <a name="to-delete-a-pull-subscription-to-a-merge-publication"></a>Para excluir uma assinatura pull em uma publicação de mesclagem.  
  
1.  No Assinante no banco de dados de assinatura, execute [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql). Especifique **@publication**, **@publisher**, e **@publisher_db**.  
  
2.  No Publicador no banco de dados de publicação, execute [sp_dropmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql). Especifique **@publication**, **@subscriber**, e **@subscriber_db**. Especifique um valor de **pull** para **@subscription_type**. (Opcional) Se o Distribuidor não puder ser acessado, especifique um valor de **1** para **@ignore_distributor** para excluir a assinatura sem remover objetos relacionados no Distribuidor.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 O exemplo a seguir exclui uma nova assinatura pull para uma publicação transacional. O primeiro lote é executado no Assinante e o segundo no Publicador.  
  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/droptranpullsub.sql#sp_droptranpullsubscription)]  
  
 [!code-sql[HowTo#sp_droptransubscription](../../snippets/tsql/SQL15/replication/howto/tsql/droptranpullsub.sql#sp_droptransubscription)]  
  
 O exemplo a seguir exclui uma assinatura pull em uma publicação de mesclagem. O primeiro lote é executado no Assinante e o segundo no Publicador.  
  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepullsub.sql#sp_dropmergepullsubscription)]  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepullsub.sql#sp_dropmergesubscription)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Você pode criar assinaturas pull programaticamente, usando o RMO (Replication Management Objects). As classes RMO que você usa para excluir uma assinatura pull dependem do tipo de publicação para a qual a assinatura pull é inscrita.  
  
#### <a name="to-delete-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para excluir uma assinatura pull em uma publicação de instantâneo ou transacional  
  
1.  Crie conexões para o Assinante e Publicador, usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription> e defina <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>e as propriedades <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> . Use a conexão de Assinante da etapa 1 para definir a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
3.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para verificar se a assinatura existe. Se o valor dessa propriedade for `false`, as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> .  
  
5.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication> usando a conexão com o Publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se esse método retornar `false`, as propriedades especificadas na etapa 5 estão incorretas ou a publicação não existe no servidor.  
  
7.  Chame o método <xref:Microsoft.SqlServer.Replication.TransPublication.RemovePullSubscription%2A> . Especifique o nome do Assinante e o banco de dados de assinatura para o *subscriber* e parâmetros *subscriberDB* .  
  
#### <a name="to-delete-a-pull-subscription-to-a-merge-publication"></a>Para excluir uma assinatura pull em uma publicação de mesclagem.  
  
1.  Crie conexões para o Assinante e Publicador, usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> e defina <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>e as propriedades <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> . Use a conexão da etapa 1 para definir a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
3.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para verificar se a assinatura existe. Se o valor dessa propriedade for `false`, as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> .  
  
5.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> usando a conexão com o Publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se esse método retornar `false`, as propriedades especificadas na etapa 5 estão incorretas ou a publicação não existe no servidor.  
  
7.  Chame o método <xref:Microsoft.SqlServer.Replication.MergePublication.RemovePullSubscription%2A> . Especifique o nome do Assinante e o banco de dados de assinatura para o *subscriber* e parâmetros *subscriberDB* .  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo exclui uma assinatura pull a uma publicação transacional e remove o registro de assinatura no Publicador.  
  
 [!code-csharp[HowTo#rmo_DropTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_droptranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_droptranpullsub)]  
  
 Esse exemplo exclui uma assinatura pull para uma publicação de mesclagem e remove o registro de assinatura no Publicador.  
  
 [!code-csharp[HowTo#rmo_DropMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropmergepullsub)]  
  
## <a name="see-also"></a>Consulte Também  
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)  
  
  
