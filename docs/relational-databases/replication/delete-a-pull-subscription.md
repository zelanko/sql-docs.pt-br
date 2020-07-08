---
title: Excluir uma assinatura pull | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 78c9ee665d35e4e6777186db9c506de16e02acf8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85654098"
---
# <a name="delete-a-pull-subscription"></a>Excluir uma assinatura pull
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Este tópico descreve como excluir uma assinatura pull no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para excluir uma assinatura pull, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
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
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As assinaturas pull podem ser excluídas programaticamente, por meio de procedimentos armazenados de replicação. Os procedimentos armazenados usados dependem do tipo de publicação ao qual a assinatura pertence.  
  
#### <a name="to-delete-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para excluir uma assinatura pull em uma publicação de instantâneo ou transacional  
  
1.  No Assinante no banco de dados de assinatura, execute [sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md). Especifique **\@publication**, **\@publisher** e **\@publisher_db**.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). Especifique **\@publication** e **\@subscriber**. Especifique um valor igual a **all** em **\@article**. (Opcional) Se o Distribuidor não puder ser acessado, especifique um valor igual a **1** em **\@ignore_distributor** para excluir a assinatura sem remover objetos relacionados no Distribuidor.  
  
#### <a name="to-delete-a-pull-subscription-to-a-merge-publication"></a>Para excluir uma assinatura pull em uma publicação de mesclagem.  
  
1.  No Assinante no banco de dados de assinatura, execute [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md). Especifique **\@publication**, **\@publisher** e **\@publisher_db**.  
  
2.  No Publicador no banco de dados de publicação, execute [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md). Especifique **\@publication**, **\@subscriber** e **\@subscriber_db**. Especifique um valor de **pull** para **\@subscription_type**. (Opcional) Se o Distribuidor não puder ser acessado, especifique um valor igual a **1** em **\@ignore_distributor** para excluir a assinatura sem remover objetos relacionados no Distribuidor.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 O exemplo a seguir exclui uma nova assinatura pull para uma publicação transacional. O primeiro lote é executado no Assinante e o segundo no Publicador.  
  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_1.sql)]  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_2.sql)]  
  
 O exemplo a seguir exclui uma assinatura pull em uma publicação de mesclagem. O primeiro lote é executado no Assinante e o segundo no Publicador.  
  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_3.sql)]  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_4.sql)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Você pode criar assinaturas pull programaticamente, usando o RMO (Replication Management Objects). As classes RMO que você usa para excluir uma assinatura pull dependem do tipo de publicação para a qual a assinatura pull é inscrita.  
  
#### <a name="to-delete-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para excluir uma assinatura pull em uma publicação de instantâneo ou transacional  
  
1.  Crie conexões para o Assinante e Publicador, usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription> e defina <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>e as propriedades <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> . Use a conexão de Assinante da etapa 1 para definir a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
3.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para verificar se a assinatura existe. Se o valor dessa propriedade for **false**, as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> .  
  
5.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication> usando a conexão com o Publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se esse método retornar **false**, as propriedades especificadas na etapa 5 estão incorretas ou a publicação não existe no servidor.  
  
7.  Chame o método <xref:Microsoft.SqlServer.Replication.TransPublication.RemovePullSubscription%2A> . Especifique o nome do Assinante e o banco de dados de assinatura para o *subscriber* e parâmetros *subscriberDB* .  
  
#### <a name="to-delete-a-pull-subscription-to-a-merge-publication"></a>Para excluir uma assinatura pull em uma publicação de mesclagem.  
  
1.  Crie conexões para o Assinante e Publicador, usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> e defina <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>e as propriedades <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> . Use a conexão da etapa 1 para definir a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
3.  Verifique a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> para verificar se a assinatura existe. Se o valor dessa propriedade for **false**, as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> .  
  
5.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> usando a conexão com o Publicador da etapa 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> e <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
6.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> . Se esse método retornar **false**, as propriedades especificadas na etapa 5 estão incorretas ou a publicação não existe no servidor.  
  
7.  Chame o método <xref:Microsoft.SqlServer.Replication.MergePublication.RemovePullSubscription%2A> . Especifique o nome do Assinante e o banco de dados de assinatura para o *subscriber* e parâmetros *subscriberDB* .  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo exclui uma assinatura pull a uma publicação transacional e remove o registro de assinatura no Publicador.  
  
 [!code-cs[HowTo#rmo_DropTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpullsub)]  
  
 Esse exemplo exclui uma assinatura pull para uma publicação de mesclagem e remove o registro de assinatura no Publicador.  
  
 [!code-cs[HowTo#rmo_DropMergePullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepullsub)]  
  
## <a name="see-also"></a>Consulte Também  
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
