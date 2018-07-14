---
title: Classe de evento Broker:Forwarded Message Sent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Forwarded Message Sent event class
ms.assetid: d0ef74d9-a4ef-4918-aa21-6b267e85569f
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1e6db9afb690f2819be36f9308ecf9de2ae81999
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217406"
---
# <a name="brokerforwarded-message-sent-event-class"></a>classe de evento Broker:Forwarded Message Sent
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento Broker:Forwarded Message Sent quando o Service Broker encaminha uma mensagem.  
  
## <a name="brokerforwarded-message-sent-event-class-data-columns"></a>Colunas de dados da classe de evento Broker:Forwarded Message Sent  
  
|Coluna de dados|Tipo|Description|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|BigintData1|`bigint`|Número de sequência da mensagem.|52|não|  
|ClientProcessID|`int`|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|DatabaseID|`int`|A ID do banco de dados especificada pela instrução de *banco de dados* USE ou a ID do banco de dados padrão se nenhuma instrução de *banco de dados*USE tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados Server Name for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DBUserName|`nvarchar`|A ID da instância do Broker em cujo serviço se originou a mensagem.|40|não|  
|EventClass|`int`|O tipo de classe de evento capturado. Sempre 139 para Broker:Forwarded Message Sent.|27|não|  
|EventSequence|`int`|Número de sequência para esse evento.|51|não|  
|FileName|`nvarchar`|O nome do serviço a que se destina a mensagem.|36|não|  
|GUID|`uniqueidentifier`|A ID de conversa da caixa de diálogo. Esse identificador é transmitido como parte da mensagem e é compartilhado por ambos os lados da conversa.|54|não|  
|HostName|`nvarchar`|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IndexID|`int`|O número de saltos restantes para a mensagem encaminhada.|24|não|  
|IntegerData|`int`|O número de fragmentos da mensagem encaminhada.|25|não|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|não|  
|LoginSid|`image`|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|ObjectId|`int`|Valor do tempo de vida da mensagem no momento de seu encaminhamento.|22|não|  
|ObjectName|`nvarchar`|O ID da mensagem encaminhada.|34|não|  
|OwnerName|`nvarchar`|O identificador do Broker ao qual a mensagem se destina.|37|não|  
|RoleName|`nvarchar`|A função do identificador de conversa. Um dos seguintes:<br /><br /> Initiator. Este Broker iniciou a conversa.<br /><br /> Target. Este Broker é o destino da conversa.|38|não|  
|ServerName|`nvarchar`|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|SPID|`int`|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|StartTime|`datetime`|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|Êxito|`int`|O tempo gasto pelo processo de encaminhamento.|23|não|  
|TargetLoginName|`nvarchar`|O endereço de rede para o qual a instância enviou a mensagem. Note que pode diferir do destino final da mensagem.|42|não|  
|TargetUserName|`nvarchar`|O nome do serviço que iniciou a mensagem.|39|não|  
|TransactionID|`bigint`|ID da transação atribuída pelo sistema.|4|não|  
  
  
