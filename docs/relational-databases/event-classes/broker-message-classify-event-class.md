---
title: Classe de evento Broker:Message Classify | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Broker:Message Classify event class
ms.assetid: e51f3351-1239-4c41-b87c-1dd86968e027
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3831b624c5fd115ed7b3a30c7a24a8ed4aec9d46
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="brokermessage-classify-event-class"></a>classe de evento Broker:Message Classify
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento **Broker:Message Classify** quando o Broker Service determina o roteamento de uma mensagem.  
  
## <a name="brokermessage-classify-event-class-data-columns"></a>Colunas de dados da classe de evento Broker:Message Classify  
  
|Coluna de dados|Tipo de dados|Description|Número da coluna|Filtrável|  
|-----------------|---------------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**ClientProcessID**|**int**|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|**DatabaseID**|**int**|A ID do banco de dados especificada pela instrução USE *database* ou a ID do banco de dados padrão se nenhuma instrução USE *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**EventClass**|**int**|O tipo de classe de evento capturado. Sempre **141** para **Broker:Message Classify**.|27|não|  
|**EventSequence**|**int**|Número de sequência para esse evento.|51|não|  
|**EventSubClass**|**nvarchar**|O tipo de subclasse de evento, fornecendo mais informações sobre cada classe de evento. Essa coluna pode conter os valores a seguir.<br /><br /> **Local**: a rota escolhida tem o endereço LOCAL.<br /><br /> **Remoto**:                 a rota escolhida tem um endereço diferente de LOCAL.<br /><br /> **Atrasado**:                a mensagem está atrasada porque o encaminhamento está desabilitado ou porque não existe rota correspondente.|21|Sim|  
|**FileName**|**nvarchar**|O nome do serviço para o qual se destina a mensagem.|36|não|  
|**GUID**|**uniqueidentifier**|A ID de conversa da caixa de diálogo. Esse identificador é transmitido como parte da mensagem e é compartilhado por ambos os lados da conversa.|54|não|  
|**HostName**|**nvarchar**|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|não|  
|**LoginSid**|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**OwnerName**|**nvarchar**|O identificador do Broker ao qual a mensagem se destina.|37|não|  
|**RoleName**|**nvarchar**|Indica se a mensagem foi recebida da rede ou se originou nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|38|não|  
|**ServerName**|**nvarchar**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|**SPID**|**int**|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|**Start Time**|**datetime**|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|**TargetUserName**|**nvarchar**|O endereço de rede do próximo Broker de salto.|39|não|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|não|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
