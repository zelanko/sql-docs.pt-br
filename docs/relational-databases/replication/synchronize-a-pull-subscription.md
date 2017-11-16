---
title: Sincronizar uma assinatura pull | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pull subscriptions [SQL Server replication], synchronizing
- synchronization [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
ms.assetid: 3ca24b23-fdc3-408e-8208-a2ace48fc8e3
caps.latest.revision: "45"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 378cb06700c6bce0dcfd5971b1a84cc4a7786770
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="synchronize-a-pull-subscription"></a>Sincronizar uma assinatura pull
  Este tópico descreve como sincronizar uma assinatura pull no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md), ou RMO (Replication Management Objects).  
  
 **Neste tópico**  
  
-   **Para sincronizar uma assinatura pull, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Replication Agents](#ReplProg)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Assinaturas são sincronizadas pelo Agente de Distribuição (para replicação transacional e de instantâneo) ou pelo Agente de Mesclagem (para replicação de mesclagem). Os agentes podem ser executados continuamente, sob demanda ou em um agendamento. Para obter mais informações sobre como especificar agendas de sincronização, consulte [Especificar agendas de sincronização](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
 Sincronize uma assinatura em demanda na pasta **Assinaturas Locais** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-synchronize-a-pull-subscription-on-demand-in-management-studio"></a>Para sincronizar uma assinatura pull sob demanda no Management Studio  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com o botão direito do mouse na assinatura a ser sincronizada e clique em **Exibir Status da Sincronização**.  
  
4.  Na caixa de diálogo **Exibir Status da Sincronização – \<Subscriber>:\<SubscriptionDatabase>**, clique em **Iniciar**. Quando a sincronização estiver concluída, a mensagem **Sincronização concluída** será exibida.  
  
5.  Clique em **Fechar**.  
  
##  <a name="ReplProg"></a> Replication Agents  
 As assinaturas pull podem ser sincronizadas programaticamente e sob demanda chamando o arquivo executável do agente de replicação apropriado do prompt de comando. O arquivo executável do agente de replicação chamado dependerá do tipo de publicação para a qual a assinatura pull pertence. Para obter mais informações, consulte [Replication Agents](../../relational-databases/replication/agents/replication-agents.md).  
  
> [!NOTE]  
>  Os agentes de replicação conectam-se ao servidor local usando as credenciais de Autenticação do Windows do usuário que inicializou o agente a partir do prompt de comando. Estas credenciais de Windows também são usadas ao conectar a servidores remotos que usam Autenticação Integrada do Windows.  
  
#### <a name="to-start-the-distribution-agent-from-the-command-prompt-or-from-a-batch-file"></a>Para iniciar o agente de distribuição no prompt de comando ou de um arquivo em lotes  
  
1.  Do prompt de comando ou em um arquivo em lote, inicie o [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md) executando **distrib.exe**, especificando os seguintes argumentos de linha de comando:  
  
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
  
1.  Do prompt de comando ou em um arquivo em lotes, inicie o [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md) executando **replmerg.exe**, especificando os seguintes argumentos de linha de comando:  
  
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
  
```  
 -- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks  
SET SubscriptionDB=AdventureWorksReplica   
SET Publication=AdvWorksProductsTran  
  
-- Start the Distribution Agent.  
-- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\100\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 1;  
```  
  
 O exemplo a seguir inicia o Agente de Mesclagem para sincronizar uma assinatura pull. Todas as conexões são feitas usando a Autenticação do Windows.  
  
```  
-- Declare the variables.  
SET Publisher=%instancename%  
SET Subscriber=%instancename%  
SET PublicationDB=AdventureWorks  
SET SubscriptionDB=AdventureWorksReplica   
SET Publication=AdvWorksSalesOrdersMerge  
  
--Start the Merge Agent with concurrent upload and download processes.  
-- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\100\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
```  
  
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
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as demais propriedades do objeto. Se esse método retornar **false**, verifique se a assinatura existe.  
  
4.  Inicie o Distribution Agent no Assinante de uma das seguintes maneiras:  
  
    -   Chame o método <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizeWithJob%2A> na instância de <xref:Microsoft.SqlServer.Replication.TransPullSubscription> da etapa 2. Esse método inicia o Distribution Agent em modo assíncrono e o controle retorna imediatamente para o seu aplicativo enquanto o trabalho do agente está em execução. Você não poderá chamar este método para Assinantes do [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] ou se a assinatura foi criada com um valor de **false** for <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (o padrão).  
  
    -   Obtenha uma instância de classe <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> da propriedade <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> , e chame o método <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> . Esse método inicia o agente de forma síncrona e o controle permanece com o trabalho do agente em execução. Durante execução síncrona, você pode manipular o evento <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> enquanto o agente está em execução.  
  
        > [!NOTE]  
        >  Se você especificou um valor **false** for <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (o padrão) quando criou a assinatura pull, também precisará especificar <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Distributor%2A>, <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorSecurityMode%2A>e, opcionalmente, <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorLogin%2A> e <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorPassword%2A> porque os metadados relativos ao trabalho do agente para a assinatura não estão disponíveis em [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md).  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-merge-publication"></a>Para sincronizar uma assinatura pull para publicação de mesclagem  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância de classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription> , e defina as propriedades a seguir:  
  
    -   O nome do banco de dados da assinatura para <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   O nome da publicação à qual a assinatura pertence para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   Nome do banco de dados publicado para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   O nome do Publicador para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   A conexão criada na etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as demais propriedades do objeto. Se esse método retornar **false**, verifique se a assinatura existe.  
  
4.  Inicie o Merge Agent no Assinante de uma das seguintes maneiras:  
  
    -   Chame o método <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizeWithJob%2A> na instância de <xref:Microsoft.SqlServer.Replication.MergePullSubscription> da etapa 2. Esse método inicia o Merge Agent em modo assíncrono e o controle retorna imediatamente para o seu aplicativo enquanto o trabalho do agente está em execução. Você não poderá chamar este método para Assinantes do [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] ou se a assinatura foi criada com um valor de **false** for <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (o padrão).  
  
    -   Obtenha uma instância de classe <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> da propriedade <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> , e chame o método <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> . Esse método inicia o Merge Agent de forma síncrona e o controle permanece com o trabalho do agente em execução. Durante execução síncrona, você pode manipular o evento <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> enquanto o agente está em execução.  
  
        > [!NOTE]  
        >  Se você especificou um valor **false** for <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (o padrão) quando criou a assinatura pull, também precisará especificar <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Distributor%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.HostName%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriptionType%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.ExchangeType%2A>e, opcionalmente, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A>e <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A> porque os metadados relativos ao trabalho do agente para a assinatura não estão disponíveis em [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md).  
  
###  <a name="PShellExample"></a> Exemplos (RMO)  
 Esse exemplo sincroniza a assinatura pull para uma publicação transacional, onde o agente é iniciado em modo assíncrono usando o trabalho do agente.  
  
```csharp  
// Define server, publication, and database names.  
String subscriberName = subscriberInstance;  
String publisherName = publisherInstance;  
String publicationName = "AdvWorksProductTran";  
String publicationDbName = "AdventureWorks";  
String subscriptionDbName = "AdventureWorksReplica";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
TransPullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define subscription properties.  
    subscription = new TransPullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription and the job exists, start the agent job.  
    if (subscription.LoadProperties() && subscription.AgentJobId != null)  
    {  
        subscription.SynchronizeWithJob();  
    }  
    else  
    {  
        // Do something here if the subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exists on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Do appropriate error handling here.  
    throw new ApplicationException("The subscription could not be synchronized.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksProductTran"  
Dim publicationDbName As String = "AdventureWorks"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As TransPullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define subscription properties.  
    subscription = New TransPullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription and the job exists, start the agent job.  
    If subscription.LoadProperties() And Not subscription.AgentJobId Is Nothing Then  
        subscription.SynchronizeWithJob()  
    Else  
        ' Do something here if the subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exists on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Do appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be synchronized.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 Esse exemplo sincroniza a assinatura pull com uma publicação transacional, em que o agente é iniciado de forma síncrona.  
  
```csharp  
// Define the server, publication, and database names.  
string subscriberName = subscriberInstance;  
string publisherName = publisherInstance;  
string publicationName = "AdvWorksProductTran";  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
TransPullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define the pull subscription.  
    subscription = new TransPullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription exists, then start the synchronization.  
    if (subscription.LoadProperties())  
    {  
        // Check that we have enough metadata to start the agent.  
        if (subscription.PublisherSecurity != null)  
        {  
            // Synchronously start the Distribution Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize();  
        }  
        else  
        {  
            throw new ApplicationException("There is insufficent metadata to " +  
                "synchronize the subscription. Recreate the subscription with " +  
                "the agent job or supply the required agent properties at run time.");  
        }  
    }  
    else  
    {  
        // Do something here if the pull subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exist on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement appropriate error handling here.  
    throw new ApplicationException("The subscription could not be " +  
        "synchronized. Verify that the subscription has " +  
        "been defined correctly.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define the server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksProductTran"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As TransPullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define the pull subscription.  
    subscription = New TransPullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription exists, then start the synchronization.  
    If subscription.LoadProperties() Then  
        ' Check that we have enough metadata to start the agent.  
        If Not subscription.PublisherSecurity Is Nothing Then  
  
            ' Write agent output to a log file.  
            subscription.SynchronizationAgent.Output = "distagent.log"  
            subscription.SynchronizationAgent.OutputVerboseLevel = 2  
  
            ' Synchronously start the Distribution Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize()  
        Else  
            Throw New ApplicationException("There is insufficent metadata to " + _  
             "synchronize the subscription. Recreate the subscription with " + _  
             "the agent job or supply the required agent properties at run time.")  
        End If  
    Else  
        ' Do something here if the pull subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exist on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Implement appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be " + _  
     "synchronized. Verify that the subscription has " + _  
     "been defined correctly.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 Esse exemplo sincroniza a assinatura pull para uma publicação de mesclagem, onde o agente é iniciado em modo assíncrono usando o trabalho do agente.  
  
```csharp  
// Define server, publication, and database names.  
String subscriberName = subscriberInstance;  
String publisherName = publisherInstance;  
String publicationName = "AdvWorksSalesOrdersMerge";  
String publicationDbName = "AdventureWorks";  
String subscriptionDbName = "AdventureWorksReplica";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define subscription properties.  
    subscription = new MergePullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription and the job exists, start the agent job.  
    if (subscription.LoadProperties() && subscription.AgentJobId != null)  
    {  
        subscription.SynchronizeWithJob();  
    }  
    else  
    {  
        // Do something here if the subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exists on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Do appropriate error handling here.  
    throw new ApplicationException("The subscription could not be synchronized.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim publicationDbName As String = "AdventureWorks"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define subscription properties.  
    subscription = New MergePullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription and the job exists, start the agent job.  
    If subscription.LoadProperties() And Not subscription.AgentJobId Is Nothing Then  
        subscription.SynchronizeWithJob()  
    Else  
        ' Do something here if the subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exists on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Do appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be synchronized.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 Esse exemplo sincroniza a assinatura pull com uma publicação de mesclagem, em que o agente é iniciado de forma síncrona.  
  
```csharp  
// Define the server, publication, and database names.  
string subscriberName = subscriberInstance;  
string publisherName = publisherInstance;  
string publicationName = "AdvWorksSalesOrdersMerge";  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
MergePullSubscription subscription;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define the pull subscription.  
    subscription = new MergePullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription exists, then start the synchronization.  
    if (subscription.LoadProperties())  
    {  
        // Check that we have enough metadata to start the agent.  
        if (subscription.PublisherSecurity != null || subscription.DistributorSecurity != null)  
        {  
            // Synchronously start the Merge Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize();  
        }  
        else  
        {  
            throw new ApplicationException("There is insufficent metadata to " +  
                "synchronize the subscription. Recreate the subscription with " +  
                "the agent job or supply the required agent properties at run time.");  
        }  
    }  
    else  
    {  
        // Do something here if the pull subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exist on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement appropriate error handling here.  
    throw new ApplicationException("The subscription could not be " +  
        "synchronized. Verify that the subscription has " +  
        "been defined correctly.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define the server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As MergePullSubscription  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define the pull subscription.  
    subscription = New MergePullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription exists, then start the synchronization.  
    If subscription.LoadProperties() Then  
        ' Check that we have enough metadata to start the agent.  
        If Not subscription.PublisherSecurity Is Nothing Or subscription.DistributorSecurity Is Nothing Then  
  
            ' Output agent messages to the console.   
            subscription.SynchronizationAgent.OutputVerboseLevel = 1  
            subscription.SynchronizationAgent.Output = ""  
  
            ' Synchronously start the Merge Agent for the subscription.  
            subscription.SynchronizationAgent.Synchronize()  
        Else  
            Throw New ApplicationException("There is insufficent metadata to " + _  
             "synchronize the subscription. Recreate the subscription with " + _  
             "the agent job or supply the required agent properties at run time.")  
        End If  
    Else  
        ' Do something here if the pull subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exist on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Implement appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be " + _  
     "synchronized. Verify that the subscription has " + _  
     "been defined correctly.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
 Esse exemplo sincroniza a assinatura pull para uma publicação de mesclagem usando sincronização da Web. A assinatura foi criada sem o trabalho do agente e metadados relativos à assinatura, assim o agente deve ser iniciado de forma síncrona e as informações de assinatura adicionais serão fornecidas.  
  
```csharp  
// Define the server, publication, and database names.  
string subscriberName = subscriberInstance;  
string publisherName = publisherInstance;  
string distributorName = distributorInstance;  
string publicationName = "AdvWorksSalesOrdersMerge";  
string subscriptionDbName = "AdventureWorksReplica";  
string publicationDbName = "AdventureWorks";  
string hostname = @"adventure-works\garrett1";  
string webSyncUrl = "https://" + publisherInstance + "/SalesOrders/replisapi.dll";  
  
// Create a connection to the Subscriber.  
ServerConnection conn = new ServerConnection(subscriberName);  
  
MergePullSubscription subscription;  
MergeSynchronizationAgent agent;  
  
try  
{  
    // Connect to the Subscriber.  
    conn.Connect();  
  
    // Define the pull subscription.  
    subscription = new MergePullSubscription();  
    subscription.ConnectionContext = conn;  
    subscription.DatabaseName = subscriptionDbName;  
    subscription.PublisherName = publisherName;  
    subscription.PublicationDBName = publicationDbName;  
    subscription.PublicationName = publicationName;  
  
    // If the pull subscription exists, then start the synchronization.  
    if (subscription.LoadProperties())  
    {  
        // Get the agent for the subscription.  
        agent = subscription.SynchronizationAgent;  
  
        // Check that we have enough metadata to start the agent.  
        if (agent.PublisherSecurityMode == null)  
        {  
            // Set the required properties that could not be returned  
            // from the MSsubscription_properties table.   
            agent.PublisherSecurityMode = SecurityMode.Integrated;  
            agent.DistributorSecurityMode = SecurityMode.Integrated;  
            agent.Distributor = publisherName;  
            agent.HostName = hostname;  
  
            // Set optional Web synchronization properties.  
            agent.UseWebSynchronization = true;  
            agent.InternetUrl = webSyncUrl;  
            agent.InternetSecurityMode = SecurityMode.Standard;  
            agent.InternetLogin = winLogin;  
            agent.InternetPassword = winPassword;  
        }  
        // Enable agent output to the console.  
        agent.OutputVerboseLevel = 1;  
        agent.Output = "";  
  
        // Synchronously start the Merge Agent for the subscription.  
        agent.Synchronize();  
    }  
    else  
    {  
        // Do something here if the pull subscription does not exist.  
        throw new ApplicationException(String.Format(  
            "A subscription to '{0}' does not exist on {1}",  
            publicationName, subscriberName));  
    }  
}  
catch (Exception ex)  
{  
    // Implement appropriate error handling here.  
    throw new ApplicationException("The subscription could not be " +  
        "synchronized. Verify that the subscription has " +  
        "been defined correctly.", ex);  
}  
finally  
{  
    conn.Disconnect();  
}  
```  
  
```vb  
' Define the server, publication, and database names.  
Dim subscriberName As String = subscriberInstance  
Dim publisherName As String = publisherInstance  
Dim publicationName As String = "AdvWorksSalesOrdersMerge"  
Dim subscriptionDbName As String = "AdventureWorksReplica"  
Dim publicationDbName As String = "AdventureWorks"  
Dim hostname As String = "adventure-works\garrett1"  
Dim webSyncUrl As String = "https://" + publisherInstance + "/SalesOrders/replisapi.dll"  
  
' Create a connection to the Subscriber.  
Dim conn As ServerConnection = New ServerConnection(subscriberName)  
  
Dim subscription As MergePullSubscription  
Dim agent As MergeSynchronizationAgent  
  
Try  
    ' Connect to the Subscriber.  
    conn.Connect()  
  
    ' Define the pull subscription.  
    subscription = New MergePullSubscription()  
    subscription.ConnectionContext = conn  
    subscription.DatabaseName = subscriptionDbName  
    subscription.PublisherName = publisherName  
    subscription.PublicationDBName = publicationDbName  
    subscription.PublicationName = publicationName  
  
    ' If the pull subscription exists, then start the synchronization.  
    If subscription.LoadProperties() Then  
        ' Get the agent for the subscription.  
        agent = subscription.SynchronizationAgent  
  
        ' Check that we have enough metadata to start the agent.  
        If agent.PublisherSecurityMode = Nothing Then  
            ' Set the required properties that could not be returned  
            ' from the MSsubscription_properties table.   
            agent.PublisherSecurityMode = SecurityMode.Integrated  
            agent.Distributor = publisherInstance  
            agent.DistributorSecurityMode = SecurityMode.Integrated  
            agent.HostName = hostname  
  
            ' Set optional Web synchronization properties.  
            agent.UseWebSynchronization = True  
            agent.InternetUrl = webSyncUrl  
            agent.InternetSecurityMode = SecurityMode.Standard  
            agent.InternetLogin = winLogin  
            agent.InternetPassword = winPassword  
        End If  
  
        ' Enable agent logging to the console.  
        agent.OutputVerboseLevel = 1  
        agent.Output = ""  
  
        ' Synchronously start the Merge Agent for the subscription.  
        agent.Synchronize()  
    Else  
        ' Do something here if the pull subscription does not exist.  
        Throw New ApplicationException(String.Format( _  
         "A subscription to '{0}' does not exist on {1}", _  
         publicationName, subscriberName))  
    End If  
Catch ex As Exception  
    ' Implement appropriate error handling here.  
    Throw New ApplicationException("The subscription could not be " + _  
     "synchronized. Verify that the subscription has " + _  
     "been defined correctly.", ex)  
Finally  
    conn.Disconnect()  
End Try  
```  
  
## <a name="see-also"></a>Consulte também  
 [Sincronizar dados](../../relational-databases/replication/synchronize-data.md)   
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
