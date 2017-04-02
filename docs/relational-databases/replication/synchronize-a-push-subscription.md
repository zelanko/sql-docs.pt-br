---
title: "Synchronize a Push Subscription | Microsoft Docs"
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
  - "synchronization [SQL Server replication], push subscriptions"
  - "subscriptions [SQL Server replication], push"
  - "assinaturas push [replicação do SQL Server], sincronizando"
ms.assetid: 0cfa7ae5-91d3-4a4f-9edf-a852d45783b5
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# Synchronize a Push Subscription
  Este tópico descreve como sincronizar uma assinatura push no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md), ou objetos de gerenciamento de replicação (RMO).  
  
 **Neste tópico**  
  
-   **Para sincronizar uma assinatura push, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Agentes de replicação](#ReplProg)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Assinaturas são sincronizadas pelo Agente de Distribuição (para replicação transacional e de instantâneo) ou pelo Agente de Mesclagem (para replicação de mesclagem). Os agentes podem ser executados continuamente, sob demanda ou em um agendamento. Para obter mais informações sobre como especificar agendas de sincronização, consulte [especificar agendas de sincronização](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
 Sincronize uma assinatura sob demea das pastas **Publicações Locais** e **Assinaturas Locais** no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e the **Todas as Assinaturas** no Replication Monitor. As assinaturas para as publicações Oracle não podem ser sincronizadas sob demanda no Assinante. Para obter informações sobre como iniciar o Monitor de replicação, consulte [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### Para sincronizar uma assinatura push sob demanda no Management Studio (no Publicador)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação com relação à qual as assinaturas serão sincronizadas.  
  
4.  Clique com botão direito a assinatura que você deseja sincronizar e, em seguida, clique em **Exibir o Status de sincronização**.  
  
5.  No **Exibir o Status de sincronização - \< assinante>: \< Banco_de_dados_de_assinatura>** caixa de diálogo, clique em **Iniciar**. Quando a sincronização estiver concluída, a mensagem **Sincronização concluída** será exibida.  
  
6.  Clique em **Fechar**.  
  
#### Para sincronizar uma assinatura push sob demanda no Management Studio (no Assinante)  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com botão direito a assinatura que você deseja sincronizar e, em seguida, clique em **Exibir o Status de sincronização**.  
  
4.  Uma mensagem é exibida sobre como estabelecer conexão com o Distribuidor. Clique em **OK**.  
  
5.  No **Exibir o Status de sincronização - \< assinante>: \< Banco_de_dados_de_assinatura>** caixa de diálogo, clique em **Iniciar**. Quando a sincronização estiver concluída, a mensagem **Sincronização concluída** será exibida.  
  
6.  Clique em **Fechar**.  
  
#### Para sincronizar uma assinatura push sob demanda no Replication Monitor  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e, depois, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique com botão direito a assinatura que você deseja sincronizar e, em seguida, clique em **Iniciar sincronização**.  
  
4.  Para exibir o progresso da sincronização, clique com o botão direito e, em seguida, clique em **Exibir detalhes**.  
  
##  <a name="ReplProg"></a> Usando agentes de replicação  
 Assinaturas push podem ser sincronizadas por programa e sob demanda chamando o arquivo executável apropriado do agente de replicação do prompt de comando. O arquivo executável do agente de replicação chamado dependerá do tipo de publicação para a qual a assinatura push pertence.  
  
#### Para iniciar o Distribution Agent para sincronizar uma assinatura push a uma publicação transacional  
  
1.  Do prompt de comando ou do arquivo de lote no Distribuidor, execute **distrib.exe**. Especifique os seguintes argumentos de linha de comando:  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType = 0**  
  
     Se você estiver usando Autenticação do SQL Server, deve-se também especificar os seguintes argumentos:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode = 0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode = 0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode = 0**  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
#### Para iniciar o Merge Agent para sincronizar uma assinatura push a uma publicação de mesclagem  
  
1.  Do prompt de comando ou do arquivo de lote no Distribuidor, execute **replmerg.exe**. Especifique os seguintes argumentos de linha de comando:  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType = 0**  
  
     Se você estiver usando Autenticação do SQL Server, deve-se também especificar os seguintes argumentos:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode = 0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode = 0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode = 0**  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
###  <a name="TsqlExample"></a> Exemplos (agentes de replicação)  
 O exemplo seguinte inicia o Agente de Distribuição para sincronizar uma assinatura push.  
  
```  
  
REM -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks2012  
SET SubscriptionDB=AdventureWorks2012Replica   
SET Publication=AdvWorksProductsTran  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4  
  
```  
  
 O exemplo a seguir inicia o Agente de Mesclagem para sincronizar uma assinatura push.  
  
```  
  
REM -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks2012  
SET SubscriptionDB=AdventureWorks2012Replica   
SET Publication=AdvWorksSalesOrdersMerge  
  
REM -- Start the Merge Agent.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE"  -Publisher %Publisher%   
-Subscriber  %Subscriber%  -Distributor %Publisher% -PublisherDB  %PublicationDB%   
-SubscriberDB %SubscriptionDB% -Publication %Publication% -PublisherSecurityMode 1   
-OutputVerboseLevel 3  -Output -SubscriberSecurityMode 1  -SubscriptionType 0   
-DistributorSecurityMode 1  
  
```  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 É possível sincronizar as assinaturas push programaticamente usando o RMO (Replication Management Objects) e o acesso de código gerenciado para as funcionalidades do agente de replicação. As classes usadas para sincronizar uma assinatura push dependem do tipo de publicação ao qual a assinatura pertence.  
  
> [!NOTE]  
>  Se quiser iniciar uma sincronização que execute autonomamente sem afetar seu aplicativo, inicie o agente em modo assíncrono. Porém, se quiser monitorar o resultado da sincronização e receber retornos de chamada do agente durante o processo de sincronização (por exemplo, se quiser exibir a barra de andamento), inicie o agente de forma síncrona. Para os Assinantes do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] , você deve iniciar o agente de forma síncrona.  
  
#### Para sincronizar uma assinatura push a um instantâneo ou publicação transacional  
  
1.  Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransSubscription> de classe e defina as seguintes propriedades:  
  
    -   O nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   O nome da publicação à qual a assinatura pertence para <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   O nome do banco de dados de assinatura para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   O nome do assinante para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   A conexão criada na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as demais propriedades. Se esse método retornar **false**, verifique se a assinatura existe.  
  
4.  Inicie o Distribution Agent no Distribuidor de uma das seguintes maneiras:  
  
    -   Chamar o <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizeWithJob%2A> método na instância do <xref:Microsoft.SqlServer.Replication.TransSubscription> da etapa 2. Esse método inicia o Distribution Agent em modo assíncrono e o controle retorna imediatamente para o seu aplicativo enquanto o trabalho do agente está em execução. Não é possível chamar esse método se a assinatura foi criada com um valor de **false** para <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A>.  
  
    -   Obter uma instância do <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> classe a partir de <xref:Microsoft.SqlServer.Replication.TransSubscription.SynchronizationAgent%2A> propriedade e chame o <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> método. Esse método inicia o agente de forma síncrona e o controle permanece com o trabalho do agente em execução. Durante a execução síncrona você pode manipular o <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> eventos enquanto o agente está em execução.  
  
#### Para sincronizar uma assinatura push a uma publicação de mesclagem  
  
1.  Criar uma conexão com o distribuidor usando a <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeSubscription> de classe e defina as seguintes propriedades:  
  
    -   O nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   O nome da publicação à qual a assinatura pertence para <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   O nome do banco de dados de assinatura para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   O nome do assinante para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   A conexão criada na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as demais propriedades. Se esse método retornar **false**, verifique se a assinatura existe.  
  
4.  Inicie o Merge Agent no Distribuidor de uma das seguintes maneiras:  
  
    -   Chamar o <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizeWithJob%2A> método na instância do <xref:Microsoft.SqlServer.Replication.MergeSubscription> da etapa 2. Esse método inicia o Merge Agent em modo assíncrono e o controle retorna imediatamente para o seu aplicativo enquanto o trabalho do agente está em execução. Não é possível chamar esse método se a assinatura foi criada com um valor de **false** para <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A>.  
  
    -   Obter uma instância do <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> classe a partir de <xref:Microsoft.SqlServer.Replication.MergeSubscription.SynchronizationAgent%2A> propriedade e chame o <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> método. Esse método inicia o Merge Agent de forma síncrona e o controle permanece com o trabalho do agente em execução. Durante a execução síncrona, você pode manipular o <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> eventos enquanto o agente está em execução.  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Este exemplo sincroniza a assinatura push a uma publicação transacional, onde o agente é iniciado de forma assíncrona usando o trabalho do agente.  
  
 [!code-csharp[HowTo#rmo_SyncTranPushSub_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_synctranpushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_synctranpushsub_withjob)]  
  
 Este exemplo sincroniza a assinatura push a uma publicação transacional, onde o agente é iniciado de forma síncrona.  
  
 [!code-csharp[HowTo#rmo_SyncTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_synctranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_synctranpushsub)]  
  
 Este exemplo sincroniza a assinatura push a uma publicação de mesclagem, onde o agente é iniciado de forma assíncrona usando o trabalho do agente.  
  
 [!code-csharp[HowTo#rmo_SyncMergePushSub_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_syncmergepushsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_syncmergepushsub_withjob)]  
  
 Este exemplo sincroniza a assinatura push a uma publicação de mesclagem, onde o agente é iniciado de forma síncrona.  
  
 [!code-csharp[HowTo#rmo_SyncMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_syncmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_syncmergepushsub)]  
  
## Consulte também  
 [Conceitos de Replication Management Objects](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  