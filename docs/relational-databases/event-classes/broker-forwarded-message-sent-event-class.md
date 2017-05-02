---
title: Classe de evento Broker:Forwarded Message Sent | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Broker:Forwarded Message Sent event class
ms.assetid: d0ef74d9-a4ef-4918-aa21-6b267e85569f
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d0462975232b9391c8cd57bc6811934f82ea5cdc
ms.lasthandoff: 04/11/2017

---
# <a name="brokerforwarded-message-sent-event-class"></a>classe de evento Broker:Forwarded Message Sent
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento Broker:Forwarded Message Sent quando o Service Broker encaminha uma mensagem.  
  
## <a name="brokerforwarded-message-sent-event-class-data-columns"></a>Colunas de dados da classe de evento Broker:Forwarded Message Sent  
  
|Coluna de dados|Tipo|Descrição|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|BigintData1|**bigint**|Número de sequência da mensagem.|52|Não|  
|ClientProcessID|**int**|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|DatabaseID|**int**|A ID do banco de dados especificada pela instrução de *banco de dados* USE ou a ID do banco de dados padrão se nenhuma instrução de *banco de dados*USE tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados Server Name for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DBUserName|**nvarchar**|A ID da instância do Broker em cujo serviço se originou a mensagem.|40|Não|  
|EventClass|**int**|O tipo de classe de evento capturado. Sempre 139 para Broker:Forwarded Message Sent.|27|Não|  
|EventSequence|**int**|Número de sequência para esse evento.|51|Não|  
|FileName|**nvarchar**|O nome do serviço a que se destina a mensagem.|36|Não|  
|GUID|**uniqueidentifier**|A ID de conversa da caixa de diálogo. Esse identificador é transmitido como parte da mensagem e é compartilhado por ambos os lados da conversa.|54|Não|  
|HostName|**nvarchar**|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IndexID|**int**|O número de saltos restantes para a mensagem encaminhada.|24|Não|  
|IntegerData|**int**|O número de fragmentos da mensagem encaminhada.|25|Não|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Não|  
|LoginSid|**image**|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|ObjectId|**int**|Valor do tempo de vida da mensagem no momento de seu encaminhamento.|22|Não|  
|ObjectName|**nvarchar**|O ID da mensagem encaminhada.|34|Não|  
|OwnerName|**nvarchar**|O identificador do Broker ao qual a mensagem se destina.|37|Não|  
|RoleName|**nvarchar**|A função do identificador de conversa. Os valores válidos são:<br /><br /> Initiator. Este Broker iniciou a conversa.<br /><br /> Target. Este Broker é o destino da conversa.|38|Não|  
|ServerName|**nvarchar**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SPID|**int**|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|StartTime|**datetime**|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|Êxito|**int**|O tempo gasto pelo processo de encaminhamento.|23|Não|  
|TargetLoginName|**nvarchar**|O endereço de rede para o qual a instância enviou a mensagem. Note que pode diferir do destino final da mensagem.|42|Não|  
|TargetUserName|**nvarchar**|O nome do serviço que iniciou a mensagem.|39|Não|  
|TransactionID|**bigint**|ID da transação atribuída pelo sistema.|4|Não|  
  
  
