---
title: Conceitos dos executáveis do agente de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- programming interfaces [SQL Server replication]
- programming [SQL Server replication], agents
- replication [SQL Server], agents and profiles
- agents [SQL Server replication], executables
- command prompt [SQL Server replication]
ms.assetid: cba476df-d4ea-44c9-bb86-81488971e328
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f02932eff39003f318d2324cce85e51e54a4a77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62724521"
---
# <a name="replication-agent-executables-concepts"></a>Conceitos dos executáveis do Replication Agent
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Os agentes de replicação podem ser controlados programaticamente das seguintes formas:  
  
-   Usando as interfaces de programação do agente gerenciado no namespace <xref:Microsoft.SqlServer.Replication>.  
  
-   Invocando arquivos executáveis do agente no prompt de comando usando um conjunto de parâmetros fornecido.  
  
 Invocar agentes de replicação diretamente do prompt de comando permite que os agentes sejam programaticamente acessados de scripts de linha de comandos existentes em arquivos em lotes. Quando um agente é invocado do prompt de comando, é executado sob a conta de segurança do Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)] do usuário que invocou o agente ou que iniciou o arquivo em lotes.  
  
 As instâncias dos agentes de replicação a seguir podem ser executadas por meio de arquivos executáveis.  
  
-   [Agente de Distribuição de Replicação](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Agente do Leitor de Log de Replicação](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Agente de Leitor de Fila de Replicação](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
-   [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
 Ao invocar agentes de replicação, você pode usar perfis de desempenho para transmitir automaticamente um conjunto definido de parâmetros para o executável do agente. Para saber mais, confira [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como invocar os agentes de replicação no prompt de comando. Os agentes de replicação também podem ser invocados usando RMO (Replication Management Objects). Para obter mais informações, consulte [Sincronizar assinaturas &#40;replicação&#41;](../../../relational-databases/replication/synchronize-data.md).  
  
> [!NOTE]  
>  As quebras de linha destes exemplos foram adicionadas para melhorar a legibilidade. Em um arquivo em lotes, devem ser feitos comandos em uma única linha.  
  
### <a name="running-the-snapshot-agent"></a>Executando o Snapshot Agent  
 Esse arquivo em lotes de exemplo invoca o Snapshot Agent no prompt de comando para gerar um instantâneo para a publicação **AdvWorksSalesOrdersMerge**. (Os scripts abaixo usam o caminho para arquivos [!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)] [versão 130]). Você deve ajustar os scripts para que eles apontem para os arquivos de sua versão do [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)].)  
  
```  
REM -- Declare variables  
SET Publisher=%InstanceName%;  
SET PublicationDB=AdventureWorks2012;   
SET Publication=AdvWorksSalesOrdersMerge;   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\130\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1 ;  
  
```  
  
### <a name="running-the-distribution-agent"></a>Executando o Distribution Agent  
 Esse arquivo em lotes de exemplo invoca o Agente de Distribuição no prompt de comando para replicar as alterações de forma contínua da publicação **AdvWorksProductTran** para um assinante push.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksProductsTran;  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4 ;  
  
```  
  
### <a name="running-the-merge-agent"></a>Executando o Merge Agent  
 Esse arquivo em lotes de exemplo invoca o Agente de Mesclagem no prompt de comando para sincronizar uma assinatura pull com a publicação **AdvWorksSalesOrdersMerge**.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksSalesOrdersMerge;  
  
REM --Start the Merge Agent with concurrent upload and download processes.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
  
```  
  
  
