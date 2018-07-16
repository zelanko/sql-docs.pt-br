---
title: Classe de evento Broker:Remote Message Ack | Microsoft Docs
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
- Broker:Remote Message Ack event class
ms.assetid: 3d67efe1-74b4-4633-b029-c6e05b19f4dc
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 49d5fba08da2929217252096ca8c2335a1f627d4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177803"
---
# <a name="brokerremote-message-ack-event-class"></a>Agente: Classe de evento Remote Message Ack
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento **Broker:Remote Message Ack** quando o [!INCLUDE[ssSB](../../includes/sssb-md.md)] envia ou recebe uma confirmação de mensagem.  
  
## <a name="brokerremote-message-ack-event-class-data-columns"></a>Colunas de dados da classe de evento Broker:Remote Message Ack  
  
|Coluna de dados|Tipo|Description|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta coluna é populada com os valores transmitidos pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**BigintData1**|**bigint**|O número de sequência da mensagem que contém a confirmação.|52|não|  
|**BigintData2**|**bigint**|O número de sequência da mensagem que está sendo confirmada.|53|não|  
|**ClientProcessID**|**int**|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|**DatabaseID**|**int**|A ID do banco de dados que é especificada pela instrução de *banco de dados* USE. Se nenhuma instrução de *banco de dados* USE tiver sido emitida para uma determinada instância, a ID do banco de dados padrão. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**EventClass**|**int**|O tipo de classe de evento capturado. Sempre **149** para **Broker:Message Ack**.|27|não|  
|**EventSequence**|**int**|Número de sequência para esse evento.|51|não|  
|**EventSubClass**|**nvarchar**|O tipo de subclasse de evento que fornece mais informações sobre cada classe de evento. Esta coluna pode conter os valores a seguir:<br /><br /> **Mensagem com confirmação enviada**<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] enviou uma confirmação como parte de uma mensagem sequenciada normal.<br /><br /> **Confirmação enviada**<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] enviou uma confirmação fora de uma mensagem sequenciada normal.<br /><br /> **Mensagem com confirmação recebida**<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] recebeu uma confirmação como parte de uma mensagem sequenciada normal.<br /><br /> **Confirmação recebida**<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] recebeu uma confirmação fora de uma mensagem sequenciada.|21|Sim|  
|**GUID**|**uniqueidentifier**|A identificação de conversa do diálogo. Esse identificador é transmitido como parte da mensagem e é compartilhado por ambos os lados da conversa.|54|não|  
|**HonorBrokerPriority**|**Int**|O valor atual da opção HONOR_BROKER_PRIORITY do banco de dados: 0 = OFF, 1 = ON.|32|Sim|  
|**HostName**|**nvarchar**|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IntegerData**|**int**|O número de fragmento da mensagem que contém a confirmação.|25|não|  
|**IntegerData2**|**int**|O número de fragmento da mensagem que está sendo confirmada.|55|não|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário.<br /><br /> 0 = usuário<br /><br /> 1 = sistema|60|não|  
|**LoginSid**|**image**|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**Prioridade**|**int**|O nível de prioridade da conversa.|5|Sim|  
|**RoleName**|**nvarchar**|A função da instância que está confirmando a mensagem. É **initiator** (iniciador) ou **target**(destino).|38|não|  
|**ServerName**|**nvarchar**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|**SPID**|**int**|A identificação de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|**StartTime**|**datetime**|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|**StarvationElevation**|**int**|A mensagem foi enviada com uma prioridade mais alta que a prioridade configurada para a conversa: 0 = false, 1 = true.|33|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|não|  
  
  
