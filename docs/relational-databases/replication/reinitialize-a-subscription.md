---
title: "Reinicializar uma assinatura | Microsoft Docs"
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
  - "inicializando assinaturas [replicação do SQL Server], reinicializando"
  - "assinaturas [replicação do SQL Server], reinicializando"
  - "reinicializando assinaturas"
ms.assetid: ca3625c5-c62e-4ab7-9829-d511f838e385
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Reinicializar uma assinatura
  Este tópico descreve como reinicializar uma assinatura no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o RMO (Replication Management Objects). Assinaturas individuais podem ser marcadas para reinicialização, para que durante a próxima sincronização, um novo instantâneo seja aplicado.  
  
 **Neste tópico**  
  
-   **Para reinicializar uma assinatura, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Reinicializar uma assinatura é um processo em duas partes:  
  
1.  Uma única assinatura ou todas as assinaturas de uma publicação são *marcadas* para reinicialização. Marcar assinaturas para reinicialização no **reinicializar assinaturas** caixa de diálogo, que está disponível a partir de **publicações locais** pasta e o **assinaturas locais** pasta no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também pode marcar assinaturas da guia **Todas as Assinaturas** e o nó de publicações no Replication Monitor. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md). Ao marcar uma assinatura para reinicialização, você tem as seguintes opções:  
  
     **Usar o instantâneo atual**  
     Selecione para aplicar o instantâneo atual ao Assinante da próxima vez que o Distribution Agent ou Merge Agent forem executados. Se não houver nenhum instantâneo válido disponível, essa opção não poderá ser selecionada.  
  
     **Usar um novo instantâneo**  
     Selecione para reinicializar a assinatura com um novo instantâneo. O instantâneo só poderá ser aplicado ao Assinante depois de ser gerado pelo Snapshot Agent. Se o Snapshot Agent estiver configurado para execução agendada, a assinatura não será reinicializada até que a próxima execução agendada do Snapshot Agent tenha ocorrido. Selecione **Gerar o novo instantâneo agora** para iniciar o Snapshot Agent imediatamente.  
  
     **Carregar alterações não sincronizadas antes da reinicialização**  
     Somente replicação de mesclagem. Selecione para carregar quaisquer alterações pendentes do banco de dados de assinatura antes que os dados no Assinante sejam substituídos com um instantâneo.  
  
     Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
2.  Uma assinatura é reinicializada na próxima vez em for sincronizada: o Distribution Agent (para replicação transacional) ou Merge Agent (para replicação de mesclagem) aplica o instantâneo mais recente a cada Assinante que tenha uma assinatura marcada para reinicialização. Para obter mais informações sobre assinaturas de sincronização, consulte [sincronizar uma assinatura Push](../../relational-databases/replication/synchronize-a-push-subscription.md) e [sincronizar uma assinatura Pull](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### Para marcar uma única assinatura push ou pull para reinicialização no Management Studio (no Publicador)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação que tem a assinatura que você quer reinicializar.  
  
4.  Clique com botão direito a assinatura e, em seguida, clique em **reinicializar**.  
  
5.  No **reinicializar assinaturas** caixa de diálogo, selecione opções e, em seguida, clique em **Marcar para reinicialização**.  
  
#### Para marcar uma única assinatura pull para reinicialização no Management Studio (no Assinante)  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com botão direito a assinatura e, em seguida, clique em **reinicializar**.  
  
4.  Na caixa de diálogo de confirmação exibida, clique em **Sim**.  
  
#### Para marcar todas as assinaturas para reinicialização no Management Studio  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com botão direito a publicação com as assinaturas que deseja reinicializar e, em seguida, clique em **reinicializar todas as inscrições**.  
  
4.  No **reinicializar assinaturas** caixa de diálogo, selecione opções e, em seguida, clique em **Marcar para reinicialização**.  
  
#### Para marcar uma única assinatura push ou pull para reinicialização no Replication Monitor  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e, depois, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique com botão direito a assinatura que você deseja reinicializar e, em seguida, clique em **reinicializar assinatura**.  
  
4.  No **reinicializar assinaturas** caixa de diálogo, selecione opções e, em seguida, clique em **Marcar para reinicialização**.  
  
#### Para marcar todas as assinaturas para reinicialização no Replication Monitor  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo e, depois, expanda um Publicador.  
  
2.  Clique com botão direito a publicação com as assinaturas que deseja reinicializar e, em seguida, clique em **reinicializar todas as inscrições**.  
  
3.  No **reinicializar assinaturas** caixa de diálogo, selecione opções e, em seguida, clique em **Marcar para reinicialização**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 As assinaturas podem ser reinicializadas forma programática, usando procedimentos armazenados. O procedimento armazenado usado depende do tipo de assinatura (push ou pull) e o tipo de publicação ao qual a assinatura pertence.  
  
#### Para reinicializar uma assinatura pull para uma publicação transacional  
  
1.  No assinante no banco de dados de assinatura, execute [sp_reinitpullsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-reinitpullsubscription-transact-sql.md). Especifique **@publisher**, **@publisher_db**, e **@publication**. Isso marca a assinatura para reinicialização na próxima vez que o Distribution Agent for executado.  
  
2.  (Opcional) Iniciar o Distribution Agent no Assinante para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### Para reinicializar uma assinatura push para uma publicação transacional  
  
1.  No publicador, execute [sp_reinitsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-reinitsubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, e **@destination_db**. Isso marca a assinatura para reinicialização na próxima vez que o Distribution Agent for executado.  
  
2.  (Opcional) Iniciar o Distribution Agent no Distributor para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### Para reinicializar uma assinatura pull para uma publicação de mesclagem  
  
1.  No assinante no banco de dados de assinatura, execute [sp_reinitmergepullsubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md). Especifique **@publisher**, **@publisher_db**, e **@publication**. Para carregar alterações do assinante antes que ocorra a reinicialização, especifique um valor de **true** para **@upload_first**. Isso marca a assinatura para reinicialização na próxima vez que o Merge Agent for executado.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
2.  (Opcional) Iniciar o Merge Agent no Assinante para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### Para reinicializar uma assinatura push para uma publicação de mesclagem.  
  
1.  No publicador, execute [sp_reinitmergesubscription & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-reinitmergesubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, e **@subscriber_db**. Para carregar alterações do assinante antes que ocorra a reinicialização, especifique um valor de **true** para **@upload_first**. Isso marca a assinatura para reinicialização na próxima vez que o Distribution Agent for executado.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
2.  (Opcional) Iniciar o Merge Agent no Distributor para sincronizar a assinatura. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### Para definir a política de reinicialização ao criar uma nova publicação de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), especificando um dos seguintes valores para **@automatic_reinitialization_policy**:  
  
    -   **1** -as alterações são carregadas do assinante antes de uma assinatura é reinicializada automaticamente de acordo com uma alteração na publicação.  
  
    -   **0** -alterações no assinante serão descartadas quando uma assinatura é reinicializada automaticamente de acordo com uma alteração na publicação.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
     Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
#### Para alterar a política de reinicialização para uma publicação de mesclagem existente  
  
1.  No publicador do banco de dados de publicação, execute [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), especificando **automatic_reinitialization_policy** para **@property** e um dos seguintes valores para **@value**:  
  
    -   **1** -as alterações são carregadas do assinante antes de uma assinatura é reinicializada automaticamente de acordo com uma alteração na publicação.  
  
    -   **0** -alterações no assinante serão descartadas quando uma assinatura é reinicializada automaticamente de acordo com uma alteração na publicação.  
  
    > [!IMPORTANT]  
    >  Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
     Para obter mais informações, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 Assinaturas individuais podem ser marcadas para reinicialização, para que durante a próxima sincronização, um novo instantâneo seja aplicado. As assinaturas podem ser reinicializadas programaticamente usando o RMO (Replication Management Objects). As classes que você usa dependem do tipo da publicação às quais as assinaturas pertencem e o tipo de assinatura (ou seja, uma assinatura push ou pull).  
  
#### Para reinicializar uma assinatura pull para uma publicação transacional  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPullSubscription> de classe e defina <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>, e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar **false**, as propriedades da assinatura na etapa 2 foram definidas incorretamente ou a assinatura pull não existe.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.TransPullSubscription.Reinitialize%2A> método. Esse método marca a assinatura para reinicialização.  
  
5.  Sincronize a assinatura pull. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### Para reinicializar uma assinatura push para uma publicação transacional  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransSubscription> de classe e defina <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar **false**, as propriedades da assinatura na etapa 2 foram definidas incorretamente ou a assinatura push não existe.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.TransSubscription.Reinitialize%2A> método. Esse método marca a assinatura para reinicialização.  
  
5.  Sincronize a assinatura push. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### Para reinicializar uma assinatura pull para uma publicação de mesclagem  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePullSubscription> de classe e defina <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>, e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar **false**, as propriedades da assinatura na etapa 2 foram definidas incorretamente ou a assinatura pull não existe.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.MergePullSubscription.Reinitialize%2A> método. Passe o valor de **true** para carregar as alterações no Assinante antes da reinicialização ou um valor de **false** para reinicializar e perder as alterações pendentes no Assinante. Esse método marca a assinatura para reinicialização.  
  
    > [!NOTE]  
    >  As alterações não poderão ser carregadas se a assinatura estiver vencida. Para obter mais informações, consulte [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md).  
  
5.  Sincronize a assinatura pull. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
#### Para reinicializar uma assinatura push para uma publicação de mesclagem.  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeSubscription> de classe e defina <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, e a conexão da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto.  
  
    > [!NOTE]  
    >  Se esse método retornar **false**, as propriedades da assinatura na etapa 2 foram definidas incorretamente ou a assinatura push não existe.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.MergeSubscription.Reinitialize%2A> método. Passe o valor de **true** para carregar as alterações no Assinante antes da reinicialização ou um valor de **false** para reinicializar e perder as alterações pendentes no Assinante. Esse método marca a assinatura para reinicialização.  
  
    > [!NOTE]  
    >  As alterações não poderão ser carregadas se a assinatura estiver vencida. Para obter mais informações, consulte [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md).  
  
5.  Sincronize a assinatura push. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo reinicializa uma assinatura pull para uma publicação transacional.  
  
 [!code-csharp[HowTo#rmo_ReinitTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinittranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinittranpullsub)]  
  
 Esse exemplo reinicializa uma assinatura pull para uma publicação de mesclagem após o primeiro carregamento das alterações pendentes no Assinante.  
  
 [!code-csharp[HowTo#rmo_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinitmergepullsub_withupload)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinitmergepullsub_withupload)]  
  
## Consulte também  
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Conceitos de Replication Management Objects](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  