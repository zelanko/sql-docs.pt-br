---
title: Sincronizar uma assinatura pull | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], synchronizing
- synchronization [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
ms.assetid: 3ca24b23-fdc3-408e-8208-a2ace48fc8e3
caps.latest.revision: 44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9143c943f18c793ce7b89be8891025b20be2e092
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37160357"
---
# <a name="synchronize-a-pull-subscription"></a>Sincronizar uma assinatura pull
  Este tópico descreve como sincronizar uma assinatura pull no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [agentes de replicação](agents/replication-agents-overview.md), ou RMO (Replication Management Objects).  
  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Assinaturas são sincronizadas pelo Agente de Distribuição (para replicação transacional e de instantâneo) ou pelo Agente de Mesclagem (para replicação de mesclagem). Os agentes podem ser executados continuamente, sob demanda ou em um agendamento. Para obter mais informações sobre como especificar agendas de sincronização, consulte [Especificar agendas de sincronização](specify-synchronization-schedules.md).  
  
 Sincronize uma assinatura em demanda na pasta **Assinaturas Locais** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-synchronize-a-pull-subscription-on-demand-in-management-studio"></a>Para sincronizar uma assinatura pull sob demanda no Management Studio  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito do mouse na assinatura a ser sincronizada e clique em **Exibir Status da Sincronização**.  
  
4.  Na caixa de diálogo **Exibir Status da Sincronização – \<Subscriber>:\<SubscriptionDatabase>**, clique em **Iniciar**. Quando a sincronização estiver concluída, a mensagem **Sincronização concluída** será exibida.  
  
5.  Clique em **Fechar**.  
  
##  <a name="ReplProg"></a> Replication Agents  
 As assinaturas pull podem ser sincronizadas programaticamente e sob demanda chamando o arquivo executável do agente de replicação apropriado do prompt de comando. O arquivo executável do agente de replicação chamado dependerá do tipo de publicação para a qual a assinatura pull pertence. Para obter mais informações, consulte [Replication Agents](agents/replication-agents.md).  
  
> [!NOTE]  
>  Os agentes de replicação conectam-se ao servidor local usando as credenciais de Autenticação do Windows do usuário que inicializou o agente a partir do prompt de comando. Estas credenciais de Windows também são usadas ao conectar a servidores remotos que usam Autenticação Integrada do Windows.  
  
#### <a name="to-start-the-distribution-agent-from-the-command-prompt-or-from-a-batch-file"></a>Para iniciar o agente de distribuição no prompt de comando ou de um arquivo em lotes  
  
1.  Do prompt de comando ou em um arquivo em lote, inicie o [Replication Distribution Agent](agents/replication-distribution-agent.md) executando **distrib.exe**, especificando os seguintes argumentos de linha de comando:  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriptionType** = **1**  
  
     Se você estiver usando Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , também deverá especificar os seguintes argumentos:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
#### <a name="to-start-the-merge-agent-from-the-command-prompt-or-from-a-batch-file"></a>Para iniciar o agente de mesclagem no prompt de comando ou de um arquivo em lotes  
  
1.  Do prompt de comando ou em um arquivo em lotes, inicie o [Replication Merge Agent](agents/replication-merge-agent.md) executando **replmerg.exe**, especificando os seguintes argumentos de linha de comando:  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-PublisherSecurityMode** = **1**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType** = **1**  
  
     Se você estiver usando Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , também deverá especificar os seguintes argumentos:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
###  <a name="TsqlExample"></a> Exemplos (agentes de replicação)  
 O exemplo a seguir inicia o Agente de Distribuição para sincronizar uma assinatura pull. Todas as conexões são feitas usando a Autenticação do Windows.  
  
 [!code-sql[HowTo#bat_synctranpullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/synctranpullsub_10.bat)]  
  
 O exemplo a seguir inicia o Agente de Mesclagem para sincronizar uma assinatura pull. Todas as conexões são feitas usando a Autenticação do Windows.  
  
 [!code-sql[HowTo#bat_syncmergepullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/syncmergepullsub_10.bat)]  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 É possível sincronizar as assinaturas pull programaticamente usando o RMO (Replication Management Objects) e o acesso de código gerenciado para as funcionalidades do agente de replicação. As classes usadas para sincronizar uma assinatura pull dependem do tipo de publicação ao qual a assinatura pertence.  
  
> [!NOTE]  
>  Se quiser iniciar uma sincronização que execute autonomamente sem afetar seu aplicativo, inicie o agente em modo assíncrono. Porém, se quiser monitorar o resultado da sincronização e receber retornos de chamada do agente durante o processo de sincronização (por exemplo, se quiser exibir uma barra de progresso), inicie o agente de forma síncrona. Para os Assinantes do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] , você deve iniciar o agente de forma síncrona.  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para sincronizar uma assinatura pull com um instantâneo ou publicação transacional  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância de classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription> , e defina as propriedades a seguir:  
  
    -   O nome do banco de dados da assinatura para <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   O nome da publicação à qual a assinatura pertence para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   O nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   O nome do Publicador para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   A conexão criada na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as demais propriedades do objeto. Se esse método retornar `false`, verifique se a assinatura existe.  
  
4.  Inicie o Distribution Agent no Assinante de uma das seguintes maneiras:  
  
    -   Chame o método <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizeWithJob%2A> na instância de <xref:Microsoft.SqlServer.Replication.TransPullSubscription> da etapa 2. Esse método inicia o Distribution Agent em modo assíncrono e o controle retorna imediatamente para o seu aplicativo enquanto o trabalho do agente está em execução. Você não poderá chamar este método para Assinantes do [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] ou se a assinatura foi criada com um valor de `false` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (o padrão).  
  
    -   Obtenha uma instância de classe <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> da propriedade <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> , e chame o método <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> . Esse método inicia o agente de forma síncrona e o controle permanece com o trabalho do agente em execução. Durante execução síncrona, você pode manipular o evento <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> enquanto o agente está em execução.  
  
        > [!NOTE]  
        >  Se você tiver especificado um valor de `false` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (o padrão) quando criou a assinatura pull, você também precisará especificar <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Distributor%2A>, <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorSecurityMode%2A>e opcionalmente <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorLogin%2A> e <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorPassword%2A> porque o trabalho do agente relacionados metadados para a assinatura não estão disponível no [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql).  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-merge-publication"></a>Para sincronizar uma assinatura pull para publicação de mesclagem  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância de classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> , e defina as propriedades a seguir:  
  
    -   O nome do banco de dados da assinatura para <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   O nome da publicação à qual a assinatura pertence para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   Nome do banco de dados publicado para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   O nome do Publicador para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   A conexão criada na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as demais propriedades do objeto. Se esse método retornar `false`, verifique se a assinatura existe.  
  
4.  Inicie o Merge Agent no Assinante de uma das seguintes maneiras:  
  
    -   Chame o método <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizeWithJob%2A> na instância de <xref:Microsoft.SqlServer.Replication.MergePullSubscription> da etapa 2. Esse método inicia o Merge Agent em modo assíncrono e o controle retorna imediatamente para o seu aplicativo enquanto o trabalho do agente está em execução. Você não poderá chamar este método para Assinantes do [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] ou se a assinatura foi criada com um valor de `false` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (o padrão).  
  
    -   Obtenha uma instância de classe <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> da propriedade <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> , e chame o método <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> . Esse método inicia o Merge Agent de forma síncrona e o controle permanece com o trabalho do agente em execução. Durante execução síncrona, você pode manipular o evento <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> enquanto o agente está em execução.  
  
        > [!NOTE]  
        >  Se você tiver especificado um valor de `false` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (o padrão) quando criou a assinatura pull, você também precisará especificar <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Distributor%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.HostName%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriptionType%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.ExchangeType%2A>, e Opcionalmente <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A>, e <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A> porque o agente de metadados relativos ao trabalho para a assinatura não está disponível no [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql).  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo sincroniza a assinatura pull para uma publicação transacional, onde o agente é iniciado em modo assíncrono usando o trabalho do agente.  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub_withjob)]  
  
 Esse exemplo sincroniza a assinatura pull com uma publicação transacional, em que o agente é iniciado de forma síncrona.  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub)]  
  
 Esse exemplo sincroniza a assinatura pull para uma publicação de mesclagem, onde o agente é iniciado em modo assíncrono usando o trabalho do agente.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_withjob)]  
  
 Esse exemplo sincroniza a assinatura pull com uma publicação de mesclagem, em que o agente é iniciado de forma síncrona.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub)]  
  
 Esse exemplo sincroniza a assinatura pull para uma publicação de mesclagem usando sincronização da Web. A assinatura foi criada sem o trabalho do agente e metadados relativos à assinatura, assim o agente deve ser iniciado de forma síncrona e as informações de assinatura adicionais serão fornecidas.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_NoJobWebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_nojobwebsync)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_NoJobWebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_nojobwebsync)]  
  
## <a name="see-also"></a>Consulte também  
 [Sincronizar dados](synchronize-data.md)   
 [Criar uma assinatura pull](create-a-pull-subscription.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)  
  
  
