---
title: Reinicializar uma assinatura | Microsoft Docs
description: Saiba como reinicializar uma assinatura no SQL Server usando SQL Server Management Studio, Transact-SQL ou Replication Management Objects.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- initializing subscriptions [SQL Server replication], reinitializing
- subscriptions [SQL Server replication], reinitializing
- reinitializing subscriptions
ms.assetid: ca3625c5-c62e-4ab7-9829-d511f838e385
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 76c0c1bfc0542dce7dadc3beb047e16f64959f54
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767729"
---
# <a name="reinitialize-a-subscription"></a>Reinicializar uma assinatura
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/applies-to-version/sql-asdb.md)]
  Este tópico descreve como reinicializar uma assinatura no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o RMO (Replication Management Objects). Assinaturas individuais podem ser marcadas para reinicialização, para que durante a próxima sincronização, um novo instantâneo seja aplicado.  
  
[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]


  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Reinicializar uma assinatura é um processo em duas partes:  
  
1.  Uma única assinatura ou todas as assinaturas de uma publicação são *marcadas* para reinicialização. Marque as assinaturas para reinicialização na caixa de diálogo **Reinicializar Assinaturas**, disponível nas pastas **Publicações Locais** e **Assinaturas Locais** do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também pode marcar assinaturas da guia **Todas as Assinaturas** e o nó de publicações no Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor). Ao marcar uma assinatura para reinicialização, você tem as seguintes opções:  
  
     **Usar o instantâneo atual**  
     Selecione para aplicar o instantâneo atual ao Assinante da próxima vez que o Distribution Agent ou Merge Agent forem executados. Se não houver nenhum instantâneo válido disponível, essa opção não poderá ser selecionada.  
  
     **Usar um novo instantâneo**  
     Selecione para reinicializar a assinatura com um novo instantâneo. O instantâneo só poderá ser aplicado ao Assinante depois de ser gerado pelo Snapshot Agent. Se o Snapshot Agent estiver configurado para execução agendada, a assinatura não será reinicializada até que a próxima execução agendada do Snapshot Agent tenha ocorrido. Selecione **Gerar o novo instantâneo agora** para iniciar o Snapshot Agent imediatamente.  
  
     **Carregar alterações não sincronizadas antes da reinicialização**  
     Somente replicação de mesclagem. Selecione para carregar quaisquer alterações pendentes do banco de dados de assinatura antes que os dados no Assinante sejam substituídos com um instantâneo.  
  
     Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
2.  Uma assinatura é reinicializada na próxima vez em for sincronizada: o Distribution Agent (para replicação transacional) ou Merge Agent (para replicação de mesclagem) aplica o instantâneo mais recente a cada Assinante que tenha uma assinatura marcada para reinicialização. Para obter mais informações sobre assinaturas de sincronização, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) e [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-mark-a-single-push-or-pull-subscription-for-reinitialization-in-management-studio-at-the-publisher"></a>Para marcar uma única assinatura push ou pull para reinicialização no Management Studio (no Publicador)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação que tem a assinatura que você quer reinicializar.  
  
4.  Clique com o botão direito do mouse na assinatura e então clique em **Reinicializar**.  
  
5.  Na caixa de diálogo **Reinicializar Assinatura(s)** , selecione opções e então clique em **Marcar para Reinicialização**.  
  
#### <a name="to-mark-a-single-pull-subscription-for-reinitialization-in-management-studio-at-the-subscriber"></a>Para marcar uma única assinatura pull para reinicialização no Management Studio (no Assinante)  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito do mouse na assinatura e então clique em **Reinicializar**.  
  
4.  Na caixa de diálogo de confirmação exibida, clique em **Sim**.  
  
#### <a name="to-mark-all-subscriptions-for-reinitialization-in-management-studio"></a>Para marcar todas as assinaturas para reinicialização no Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse na publicação com as assinaturas que você deseja reinicializar e então clique em **Reinicializar Todas as Assinaturas**.  
  
4.  Na caixa de diálogo **Reinicializar Assinatura(s)** , selecione opções e então clique em **Marcar para Reinicialização**.  
  
#### <a name="to-mark-a-single-push-or-pull-subscription-for-reinitialization-in-replication-monitor"></a>Para marcar uma única assinatura push ou pull para reinicialização no Replication Monitor  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e, depois, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique com o botão direito do mouse na assinatura que deseja reinicializar e então clique em **Reinicializar Sincronização**.  
  
4.  Na caixa de diálogo **Reinicializar Assinatura(s)** , selecione opções e então clique em **Marcar para Reinicialização**.  
  
#### <a name="to-mark-all-subscriptions-for-reinitialization-in-replication-monitor"></a>Para marcar todas as assinaturas para reinicialização no Replication Monitor  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo e, depois, expanda um Publicador.  
  
2.  Clique com o botão direito do mouse na publicação com as assinaturas que você deseja reinicializar e então clique em **Reinicializar Todas as Assinaturas**.  
  
3.  Na caixa de diálogo **Reinicializar Assinatura(s)** , selecione opções e então clique em **Marcar para Reinicialização**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As assinaturas podem ser reinicializadas forma programática, usando procedimentos armazenados. O procedimento armazenado usado depende do tipo de assinatura (push ou pull) e o tipo de publicação ao qual a assinatura pertence.  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-transactional-publication"></a>Para reinicializar uma assinatura pull para uma publicação transacional  
  
1.  No Assinante, no banco de dados de assinatura, execute [sp_reinitpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitpullsubscription-transact-sql.md). Especifique **\@publisher**, **\@publisher_db** e **\@publication**. Isso marca a assinatura para reinicialização na próxima vez que o Distribution Agent for executado.  
  
2.  (Opcional) Iniciar o Distribution Agent no Assinante para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-transactional-publication"></a>Para reinicializar uma assinatura push para uma publicação transacional  
  
1.  No Publicador, execute [sp_reinitsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitsubscription-transact-sql.md). Especifique **\@publication**, **\@subscriber** e **\@destination_db**. Isso marca a assinatura para reinicialização na próxima vez que o Distribution Agent for executado.  
  
2.  (Opcional) Iniciar o Distribution Agent no Distributor para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-merge-publication"></a>Para reinicializar uma assinatura pull para uma publicação de mesclagem  
  
1.  No Assinante, no banco de dados de assinatura, execute [sp_reinitmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md). Especifique **\@publisher**, **\@publisher_db** e **\@publication**. Para fazer upload das alterações do Assinante antes que a reinicialização ocorra, especifique um valor igual a **true** em **\@upload_first**. Isso marca a assinatura para reinicialização na próxima vez que o Merge Agent for executado.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
2.  (Opcional) Iniciar o Merge Agent no Assinante para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-merge-publication"></a>Para reinicializar uma assinatura push para uma publicação de mesclagem.  
  
1.  No Publicador, execute [sp_reinitmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-reinitmergesubscription-transact-sql.md). Especifique **\@publication**, **\@subscriber** e **\@subscriber_db**. Para fazer upload das alterações do Assinante antes que a reinicialização ocorra, especifique um valor igual a **true** em **\@upload_first**. Isso marca a assinatura para reinicialização na próxima vez que o Distribution Agent for executado.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
2.  (Opcional) Iniciar o Merge Agent no Distributor para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### <a name="to-set-the-reinitialization-policy-when-creating-a-new-merge-publication"></a>Para definir a política de reinicialização ao criar uma nova publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) especificando um dos seguintes valores em **\@automatic_reinitialization_policy**:  
  
    -   **1** - alterações são carregadas do Assinante antes que a assinatura seja reinicializada automaticamente, de acordo com a alteração feita na publicação.  
  
    -   **0** - alterações no Assinante são descartadas quando uma assinatura é reinicializada automaticamente, de acordo com a alteração feita na publicação.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
     Para obter mais informações, consulte [Criar uma assinatura](../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-change-the-reinitialization-policy-for-an-existing-merge-publication"></a>Para alterar a política de reinicialização para uma publicação de mesclagem existente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) especificando **automatic_reinitialization_policy** em **\@property** e um dos seguintes valores em **\@value**:  
  
    -   **1** - alterações são carregadas do Assinante antes que a assinatura seja reinicializada automaticamente, de acordo com a alteração feita na publicação.  
  
    -   **0** - alterações no Assinante são descartadas quando uma assinatura é reinicializada automaticamente, de acordo com a alteração feita na publicação.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
     Para obter mais informações, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Assinaturas individuais podem ser marcadas para reinicialização, para que durante a próxima sincronização, um novo instantâneo seja aplicado. As assinaturas podem ser reinicializadas programaticamente usando o RMO (Replication Management Objects). As classes que você usa dependem do tipo da publicação às quais as assinaturas pertencem e o tipo de assinatura (ou seja, uma assinatura push ou pull).  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-transactional-publication"></a>Para reinicializar uma assinatura pull para uma publicação transacional  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription> , defina <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar **false**, isso significa que as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura pull não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.TransPullSubscription.Reinitialize%2A> . Esse método marca a assinatura para reinicialização.  
  
5.  Sincronize a assinatura pull. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-transactional-publication"></a>Para reinicializar uma assinatura push para uma publicação transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransSubscription> , defina <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar **false**, isso significa que as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura push não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.TransSubscription.Reinitialize%2A> . Esse método marca a assinatura para reinicialização.  
  
5.  Sincronize a assinatura push. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-merge-publication"></a>Para reinicializar uma assinatura pull para uma publicação de mesclagem  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> , defina <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar **false**, isso significa que as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura pull não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.MergePullSubscription.Reinitialize%2A> . Passe o valor de **true** para carregar as alterações no Assinante antes da reinicialização ou um valor de **false** para reinicializar e perder as alterações pendentes no Assinante. Esse método marca a assinatura para reinicialização.  
  
    > [!NOTE]  
    >  As alterações não poderão ser carregadas se a assinatura estiver vencida. Para obter mais informações, consulte [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md).  
  
5.  Sincronize a assinatura pull. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-merge-publication"></a>Para reinicializar uma assinatura push para uma publicação de mesclagem.  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeSubscription> , defina <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar **false**, isso significa que as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura push não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.MergeSubscription.Reinitialize%2A> . Passe o valor de **true** para carregar as alterações no Assinante antes da reinicialização ou um valor de **false** para reinicializar e perder as alterações pendentes no Assinante. Esse método marca a assinatura para reinicialização.  
  
    > [!NOTE]  
    >  As alterações não poderão ser carregadas se a assinatura estiver vencida. Para obter mais informações, consulte [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md).  
  
5.  Sincronize a assinatura push. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo reinicializa uma assinatura pull para uma publicação transacional.  
  
 [!code-cs[HowTo#rmo_ReinitTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinittranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinittranpullsub)]  
  
 Esse exemplo reinicializa uma assinatura pull para uma publicação de mesclagem após o primeiro carregamento das alterações pendentes no Assinante.  
  
 [!code-cs[HowTo#rmo_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinitmergepullsub_withupload)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinitmergepullsub_withupload)]  
  
## <a name="see-also"></a>Consulte Também  
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
