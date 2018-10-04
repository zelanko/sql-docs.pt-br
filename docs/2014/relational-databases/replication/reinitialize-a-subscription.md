---
title: Reinicializar uma assinatura | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- initializing subscriptions [SQL Server replication], reinitializing
- subscriptions [SQL Server replication], reinitializing
- reinitializing subscriptions
ms.assetid: ca3625c5-c62e-4ab7-9829-d511f838e385
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 738b9179143b4c6b0c986f7f6a16464980b60f8f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130326"
---
# <a name="reinitialize-a-subscription"></a>Reinicializar uma assinatura
  Este tópico descreve como reinicializar uma assinatura no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o RMO (Replication Management Objects). Assinaturas individuais podem ser marcadas para reinicialização, para que durante a próxima sincronização, um novo instantâneo seja aplicado.  
  
 **Neste tópico**  
  
-   **Para reinicializar uma assinatura, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Reinicializar uma assinatura é um processo em duas partes:  
  
1.  Uma única assinatura ou todas as assinaturas de uma publicação são *marcadas* para reinicialização. Marque as assinaturas para reinicialização na caixa de diálogo **Reinicializar Assinatura(s)** , que está disponível nas pastas **Publicações Locais** e **Assinaturas Locais** no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também pode marcar assinaturas da guia **Todas as Assinaturas** e o nó de publicações no Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor). Ao marcar uma assinatura para reinicialização, você tem as seguintes opções:  
  
     **Usar o instantâneo atual**  
     Selecione para aplicar o instantâneo atual ao Assinante da próxima vez que o Distribution Agent ou Merge Agent forem executados. Se não houver nenhum instantâneo válido disponível, essa opção não poderá ser selecionada.  
  
     **Usar um novo instantâneo**  
     Selecione para reinicializar a assinatura com um novo instantâneo. O instantâneo só poderá ser aplicado ao Assinante depois de ser gerado pelo Snapshot Agent. Se o Snapshot Agent estiver configurado para execução agendada, a assinatura não será reinicializada até que a próxima execução agendada do Snapshot Agent tenha ocorrido. Selecione **Gerar o novo instantâneo agora** para iniciar o Snapshot Agent imediatamente.  
  
     **Carregar alterações não sincronizadas antes da reinicialização**  
     Somente replicação de mesclagem. Selecione para carregar quaisquer alterações pendentes do banco de dados de assinatura antes que os dados no Assinante sejam substituídos com um instantâneo.  
  
     Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
2.  Uma assinatura é reinicializada na próxima vez em for sincronizada: o Distribution Agent (para replicação transacional) ou Merge Agent (para replicação de mesclagem) aplica o instantâneo mais recente a cada Assinante que tenha uma assinatura marcada para reinicialização. Para obter mais informações sobre assinaturas de sincronização, consulte [Synchronize a Push Subscription](synchronize-a-push-subscription.md) e [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
#### <a name="to-mark-a-single-push-or-pull-subscription-for-reinitialization-in-management-studio-at-the-publisher"></a>Para marcar uma única assinatura push ou pull para reinicialização no Management Studio (no Publicador)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
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
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
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
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As assinaturas podem ser reinicializadas forma programática, usando procedimentos armazenados. O procedimento armazenado usado depende do tipo de assinatura (push ou pull) e o tipo de publicação ao qual a assinatura pertence.  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-transactional-publication"></a>Para reinicializar uma assinatura pull para uma publicação transacional  
  
1.  No Assinante, no banco de dados de assinatura, execute [sp_reinitpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-reinitpullsubscription-transact-sql). Especifique **@publisher**, o **@publisher_db**, e **@publication**. Isso marca a assinatura para reinicialização na próxima vez que o Distribution Agent for executado.  
  
2.  (Opcional) Iniciar o Distribution Agent no Assinante para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-transactional-publication"></a>Para reinicializar uma assinatura push para uma publicação transacional  
  
1.  No Publicador, execute [sp_reinitsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-reinitsubscription-transact-sql). Especifique **@publication**, o **@subscriber**, e **@destination_db**. Isso marca a assinatura para reinicialização na próxima vez que o Distribution Agent for executado.  
  
2.  (Opcional) Iniciar o Distribution Agent no Distributor para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-merge-publication"></a>Para reinicializar uma assinatura pull para uma publicação de mesclagem  
  
1.  No Assinante, no banco de dados de assinatura, execute [sp_reinitmergepullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql). Especifique **@publisher**, o **@publisher_db**, e **@publication**. Para carregar alterações do assinante antes da reinicialização ocorra, especifique um valor de `true` para **@upload_first**. Isso marca a assinatura para reinicialização na próxima vez que o Merge Agent for executado.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
2.  (Opcional) Iniciar o Merge Agent no Assinante para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-merge-publication"></a>Para reinicializar uma assinatura push para uma publicação de mesclagem.  
  
1.  No Publicador, execute [sp_reinitmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-reinitmergesubscription-transact-sql). Especifique **@publication**, o **@subscriber**, e **@subscriber_db**. Para carregar alterações do assinante antes da reinicialização ocorra, especifique um valor de `true` para **@upload_first**. Isso marca a assinatura para reinicialização na próxima vez que o Distribution Agent for executado.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
2.  (Opcional) Iniciar o Merge Agent no Distributor para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
#### <a name="to-set-the-reinitialization-policy-when-creating-a-new-merge-publication"></a>Para definir a política de reinicialização ao criar uma nova publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql), especificando um dos valores a seguir para **@automatic_reinitialization_policy**:  
  
    -   **1** - alterações são carregadas do Assinante antes que a assinatura seja reinicializada automaticamente, de acordo com a alteração feita na publicação.  
  
    -   **0** - alterações no Assinante são descartadas quando uma assinatura é reinicializada automaticamente, de acordo com a alteração feita na publicação.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
     Para obter mais informações, consulte [Create a Publication](publish/create-a-publication.md).  
  
#### <a name="to-change-the-reinitialization-policy-for-an-existing-merge-publication"></a>Para alterar a política de reinicialização para uma publicação de mesclagem existente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando **automatic_reinitialization_policy** para **@property** e um dos seguintes valores para **@value**:  
  
    -   **1** - alterações são carregadas do Assinante antes que a assinatura seja reinicializada automaticamente, de acordo com a alteração feita na publicação.  
  
    -   **0** - alterações no Assinante são descartadas quando uma assinatura é reinicializada automaticamente, de acordo com a alteração feita na publicação.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
     Para obter mais informações, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Assinaturas individuais podem ser marcadas para reinicialização, para que durante a próxima sincronização, um novo instantâneo seja aplicado. As assinaturas podem ser reinicializadas programaticamente usando o RMO (Replication Management Objects). As classes que você usa dependem do tipo da publicação às quais as assinaturas pertencem e o tipo de assinatura (ou seja, uma assinatura push ou pull).  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-transactional-publication"></a>Para reinicializar uma assinatura pull para uma publicação transacional  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription> , defina <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar `false`, significa que as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura pull não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.TransPullSubscription.Reinitialize%2A> . Esse método marca a assinatura para reinicialização.  
  
5.  Sincronize a assinatura pull. Para obter mais informações, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-transactional-publication"></a>Para reinicializar uma assinatura push para uma publicação transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransSubscription> , defina <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar `false`, significa que as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura push não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.TransSubscription.Reinitialize%2A> . Esse método marca a assinatura para reinicialização.  
  
5.  Sincronize a assinatura push. Para obter mais informações, consulte [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-merge-publication"></a>Para reinicializar uma assinatura pull para uma publicação de mesclagem  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> , defina <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar `false`, significa que as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura pull não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.MergePullSubscription.Reinitialize%2A> . Passe o valor de `true` para carregar as alterações no Assinante antes da reinicialização ou um valor de `false` para reinicializar e perder as alterações pendentes no Assinante. Esse método marca a assinatura para reinicialização.  
  
    > [!NOTE]  
    >  As alterações não poderão ser carregadas se a assinatura estiver vencida. Para obter mais informações, consulte [Set the Expiration Period for Subscriptions](publish/set-the-expiration-period-for-subscriptions.md).  
  
5.  Sincronize a assinatura pull. Para obter mais informações, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-merge-publication"></a>Para reinicializar uma assinatura push para uma publicação de mesclagem.  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeSubscription> , defina <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar `false`, significa que as propriedades de assinatura na etapa 2 foram definidas incorretamente ou a assinatura push não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.MergeSubscription.Reinitialize%2A> . Passe o valor de `true` para carregar as alterações no Assinante antes da reinicialização ou um valor de `false` para reinicializar e perder as alterações pendentes no Assinante. Esse método marca a assinatura para reinicialização.  
  
    > [!NOTE]  
    >  As alterações não poderão ser carregadas se a assinatura estiver vencida. Para obter mais informações, consulte [Set the Expiration Period for Subscriptions](publish/set-the-expiration-period-for-subscriptions.md).  
  
5.  Sincronize a assinatura push. Para obter mais informações, consulte [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo reinicializa uma assinatura pull para uma publicação transacional.  
  
 [!code-csharp[HowTo#rmo_ReinitTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_reinittranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_reinittranpullsub)]  
  
 Esse exemplo reinicializa uma assinatura pull para uma publicação de mesclagem após o primeiro carregamento das alterações pendentes no Assinante.  
  
 [!code-csharp[HowTo#rmo_ReinitMergePullSub_WithUpload](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_reinitmergepullsub_withupload)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitMergePullSub_WithUpload](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_reinitmergepullsub_withupload)]  
  
## <a name="see-also"></a>Consulte também  
 [Reinicializar as assinaturas](reinitialize-subscriptions.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)  
  
  
