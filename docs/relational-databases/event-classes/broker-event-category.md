---
title: Categoria de evento Broker | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Broker event category
- Broker event category [SQL Server]
- event classes [SQL Server], Broker event category
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8efa6f503f552965e3885d92626e8b5da453e29b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "69494091"
---
# <a name="broker-event-category"></a>Categoria de evento Broker

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

A categoria de evento **Broker** contém eventos gerais do Service Broker.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
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
 [Categoria de evento de auditoria de segurança](/bi-reference/trace-events/security-audit-event-category)  
  
  
