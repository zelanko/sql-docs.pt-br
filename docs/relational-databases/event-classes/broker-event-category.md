---
title: Categoria de evento Broker | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Broker event category
- Broker event category [SQL Server]
- event classes [SQL Server], Broker event category
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cab6e66358d16cabb70cd2c371a8f139bd371c99
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="broker-event-category"></a>Categoria de evento Broker
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A categoria de evento **Broker** contém eventos gerais do Service Broker.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Classe de evento Broker:Activation](../../relational-databases/event-classes/broker-activation-event-class.md)|Um evento gerado quando um monitor de fila inicia um procedimento armazenado de ativação.|  
|[Classe de evento Broker:Connection](../../relational-databases/event-classes/broker-connection-event-class.md)|Um evento gerado para informar o status de uma conexão de transporte gerenciada pelo Service Broker.|  
|[Classe de evento Broker:Conversation](../../relational-databases/event-classes/broker-conversation-event-class.md)|Um evento gerado para reportar o progresso de uma conversa.|  
|[Classe de evento Broker:Conversation Group](../../relational-databases/event-classes/broker-conversation-group-event-class.md)|Um evento gerado quando o banco de dados cria ou descarta um grupo de conversa.|  
|[Classe de evento Broker:Corrupted Message](../../relational-databases/event-classes/broker-corrupted-message-event-class.md)|Um evento gerado para informar que o banco de dados recebeu uma mensagem corrompida.|  
|[Classe de evento Broker:Forwarded Message Dropped](../../relational-databases/event-classes/broker-forwarded-message-dropped-event-class.md)|Um evento gerado quando o SQL Server descarta uma mensagem do Service Broker que deveria ter sido encaminhada.|  
|[Classe de evento Broker:Forwarded Message Sent](../../relational-databases/event-classes/broker-forwarded-message-sent-event-class.md)|Um evento gerado quando o SQL Server encaminha uma mensagem do Service Broker.|  
|[Classe de evento Broker:Message Classify](../../relational-databases/event-classes/broker-message-classify-event-class.md)|Um evento gerado quando o Service Broker determina o roteamento de uma mensagem.|  
|[Classe de evento Broker:Message Drop](../../relational-databases/event-classes/broker-message-drop-event-class.md)|Um evento gerado quando o Service Broker é incapaz de reter uma mensagem recebida que deveria ter sido entregue a um serviço dessa instância.|  
|[Agente: Classe de evento Remote Message Ack](../../relational-databases/event-classes/broker-remote-message-ack-event-class.md)|Um evento gerado quando o Service Broker envia ou recebe uma confirmação de mensagem.|  
  
 Também são fornecidos dois eventos de auditoria de segurança para o Service Broker. Para obter mais informações sobre esses eventos, consulte [Classe de evento Audit Broker Login](../../relational-databases/event-classes/audit-broker-login-event-class.md) e [Classe de evento Audit Broker Conversation](../../relational-databases/event-classes/audit-broker-conversation-event-class.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Categoria de evento de auditoria de segurança](../../analysis-services/trace-events/security-audit-event-category.md)  
  
  
